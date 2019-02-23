# Hello, Debian!

* [Debian -- The Universal Operating System](https://www.debian.org/index.en.html)
* [Debian -- 通用操作系统](https://www.debian.org/index.zh-cn.html)

Debian is a free operating system (OS) for your computer. An operating system is the set of basic programs and utilities that make your computer run.

## package management

The Debian package management system has a rich history and many choices for the front end user program and back end archive access method to be used. Currently, we recommend the following.

* apt(8) for all interactive command line operations, including package installation, removal and dist-upgrades. Available since Debian Jessie (Debian 8).
* apt-get(8) for calling Debian package management system from scripts. It is also a fallback option when apt is not available (often with older Debian systems).

**Here is a summary of the simplified event flow of the package management by APT.**

* **Update** ("apt update" or "apt-get update")
* **Upgrade** ("apt upgrade" and "apt full-upgrade", or "apt-get upgrade" and "apt-get dist-upgrade")
* **Install** ("apt install …" or "apt-get install …")
* **Remove** ("apt remove …" or "apt-get remove …")
* **Purge** ("apt purge" or "apt-get purge …")

**Please check the link below for more information:**

* [Chapter 2. Debian package management](https://www.debian.org/doc/manuals/debian-reference/ch02.en.html)
* [第 2 章 Debian 软件包管理](https://www.debian.org/doc/manuals/debian-reference/ch02.zh-cn.html)

## System Upgrade

Find out current version of Debian that you are running:

```
# cat /etc/debian_version
```

Upgrading the system:

```
# apt update
# apt upgrade
```

**Please check the link below for more information:**

* [6.2. aptitude, apt-get, and apt Commands](https://www.debian.org/doc/manuals/debian-handbook/sect.apt-get.en.html#sect.apt-upgrade)
* [6.2. aptitude、apt-get和 apt 命令](https://www.debian.org/doc/manuals/debian-handbook/sect.apt-get.zh-cn.html#sect.apt-upgrade)

## SSH

SSH stands for Secure Shell and is a protocol for secure remote login and other secure network services over an insecure network.

**Tools:**

* [PuTTY](https://www.putty.org/)

**Configuration files**

The main configuration files are in the directory `/etc/ssh` :

* **ssh_config** : client configuration file
* **sshd_config** : server configuration file

**Create a new user**

It is wise to create a dummy local user with absolutely no rights on the system and use that user to login into SSH. That way no harm can be done if the user account is compromised.

```
# adduser username
```

**Change SSH listening port**

1. By default, SSH listens for connections on port 22;
2. Open the `/etc/ssh/sshd_config` file and look for the line that says: `Port 22`;
3. Change the port number and restart the SSH service: `/etc/init.d/ssh restart`.

**Allow only SSH protocol 2**

There are two versions of the SSH protocol. Using SSH protocol 2 only is much more secure; SSH protocol 1 is subject to security issues including man-in-the-middle and insertion attacks.

Edit `/etc/ssh/sshd_config` and look for the line that says: `Protocol 2,1` (Change the line so it says only protocol 2.).

**Create a custom SSH banner**

1. If you would like any user who connects to your SSH service to see a specific message, you can create a custom SSH banner. Simply create a text file (in my example in `/etc/ssh-banner.txt`) and put any kind of text message in it; for example: `This is a private SSH service.Please leave.Thanks.`
2. When done editing, save the file. In the sshd_conf file, find a line that says: `#Banner /etc/issue.net`
3. Uncomment the line and change the path to your custom SSH banner text file.

**Allow only specific users to log in via SSH**

You should not permit root logins via SSH, because this is a big and unnecessary security risk. If an attacker gains root login for your system, he can do more damage than if he gains normal user login. Configure SSH server so that root user is not allowed to log in. Find the line that says: `PermitRootLogin yes`

Change yes to no and restart the service. You can then log in with any other defined user and switch to user root if you want to become a superuser.

If you would like to have a list of users who are the only ones able to log in via SSH, you can specify them in the sshd_config file. For example, let's say I want to allow users anze, dasa, and kimy to log in via SSH. At the end of sshd_config file I would add a line like this: `AllowUsers anze dasa kimy`

**Using RSA or DSA public key authentication**

Generate the key-pair, a public-key and a private-key. The public-key will be placed on the server, and you will log in with your private-key. When asked, type your passphrase (it'll be needed for future logins, so remember it!).

Then we copy the public key (which we've generated just before) to our (remote) server. The remoteuser should not be `root` ! Choose the default non-root user as remoteuser.

Then we log in with SSh, and we copy the public key to its right place:

```
$ mkdir ~/.ssh
$ chmod 700 ~/.ssh
$ vi ~/.ssh/authorized_keys
$ chmod 600 ~/.ssh/authorized_keys
```

We have to delete the public key on the desktop, because otherwise the SSH client doesn't allow us to log in to the server.

**Disabling Password Authentication**

Disabling it is a good way to have a safer SSH-installation. Then you can log in only with a key-pair, so be careful not to lose it! It's purely optional but safe to activate! But before doing it, please make sure that key-based authentication is working out-of-the-box.

Change these lines:

```
PermitRootLogin yes
#AuthorizedKeysFile     %h/.ssh/authorized_keys
PasswordAuthentication yes
UsePAM yes
```

To these:

```
PermitRootLogin no
AuthorizedKeysFile     %h/.ssh/authorized_keys
PasswordAuthentication no
UsePAM no
```

Then running:

```
# /etc/init.d/ssh restart
```

**sftp**

create the sftp group:

```
# addgroup --gid 1099 sftp
```

Following changes to the SSH daemon configure permissions for the sftp group:

```
# vim /etc/ssh/sshd_config

Port 22

Match Group sftp, LocalPort 22
    ChrootDirectory %h
    ForceCommand internal-sftp
    AllowTcpForwarding no
    PermitTunnel no
    X11Forwarding no

    # AuthorizedKeysFile     %h/.ssh/authorized_keys
    PasswordAuthentication yes

    AllowUsers 

# /etc/init.d/ssh restart
```

The chroot directory must be owned by root.

```
# chown root:root /home/username
```

Add the `sftp` only group to each user with remote access rights.

```
# gpasswd -a username sftp
```

* [sshd_config(5)](https://www.freebsd.org/cgi/man.cgi?sshd_config(5))
* [SFTP chroot](https://wiki.archlinux.org/index.php/SFTP_chroot)

**fail2ban**

**Using TCP wrappers to allow only specific hosts to connect**

**Using iptables to allow only specific hosts to connect**

**Please check the link below for more information:**

* [Wikipedia - Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell)
* [SSH - Debian Wiki](https://wiki.debian.org/SSH)

## Apache

**Installing Apache under Debian**

```
# apt install apache2
```

**The default installation**

```
ServerRoot
    :: /etc/apache2

DocumentRoot
    :: /var/www

Apache Config Files
    :: /etc/apache2/apache2.conf
    :: /etc/apache2/ports.conf

Default VHost Config
    :: /etc/apache2/sites-available/000-default.conf, /etc/apache2/sites-enabled/000-default.conf

Module Locations
    :: /etc/apache2/mods-available, /etc/apache2/mods-enabled

ErrorLog
    :: /var/log/apache2/error.log

AccessLog
    :: /var/log/apache2/access.log

cgi-bin
    :: /usr/lib/cgi-bin

binaries(apachectl)
    :: /usr/sbin

start/stop
    :: /etc/init.d/apache2 (start|stop|restart|reload|force-reload|start-htcacheclean|stop-htcacheclean)
```

**MPM**

With Apache 2.4 in Debian the Multi-Processing Module used is no longer selected by installing one of the apache2-mpm- packages. MPM modules are enabled and disabled using the a2enmod and a2dismod commands just like with any other module. Only one MPM may be used at a time.

The default MPM used by Apache 2.4 in Debian is mpm_event. An example of switching to mpm_worker:

```
# a2dismod mpm_event
# a2enmod mpm_prefork
# /etc/init.d/apache2 restart
```

sites that need a great deal of scalability can choose to use a threaded MPM like **worker** or **event**.

sites requiring stability or compatibility with older software can use a **prefork**.

Some modules such as libapache2-mod-php5 that require using **mpm_prefork** will switch to this MPM as part of the package's post installation script.

**Configuring user directories for Apache Web Server**

Enable module:

```
# a2enmod userdir
# /etc/init.d/apache2 restart
```

**Rewrite**

Enable module:

```
# a2enmod rewrite
# /etc/init.d/apache2 restart
```

**Virtual Hosts**

Creat a new user:

```
# adduser username
```

Create directory as user (not as root):

```
$ mkdir /home/$USER/public_html log backup
```

Configuring sites-available & sites-enabled:

```
# cd /etc/apache2/sites-available/
# vim 000-default.conf
# a2ensite 000-default.conf
# /etc/init.d/apache2 restart
```

`000-default.conf`

```
<VirtualHost *:80>
    # The ServerName directive sets the request scheme, hostname and port that
    # the server uses to identify itself. This is used when creating
    # redirection URLs. In the context of virtual hosts, the ServerName
    # specifies what hostname must appear in the request's Host: header to
    # match this virtual host. For the default virtual host (this file) this
    # value is not decisive as it is used as a last resort host regardless.
    # However, you must set it for any further virtual host explicitly.

    ServerName www.
    ServerAlias 

    ServerAdmin webmaster@localhost
    DocumentRoot /home/www.example.com/public_html

    # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
    # error, crit, alert, emerg.
    # It is also possible to configure the loglevel for particular
    # modules, e.g.
    #LogLevel info ssl:warn

    ErrorLog /home/www.example.com/log/error.log
    CustomLog /home/www.example.com/log/access.log combined

    # For most configuration files from conf-available/, which are
    # enabled or disabled at a global level, it is possible to
    # include a line for only one particular virtual host. For example the
    # following line enables the CGI configuration for this host only
    # after it has been globally disabled with "a2disconf".
    #Include conf-available/serve-cgi-bin.conf
</VirtualHost>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet
```

one:

```
# vim /etc/apache2/envvars

export APACHE_RUN_USER=www-data
export APACHE_RUN_GROUP=www-data

# /etc/init.d/apache2 restart
```

multiple:

```
# aptitude install libapache2-mpm-itk

# a2enmod mpm_itk

# vim 000-default.conf

AssignUserID uid gid

# /etc/init.d/apache2 restart
```

* [The Apache 2 ITK MPM](http://mpm-itk.sesse.net/)
* [Q1](https://stackoverflow.com/questions/5165183/apache-permissions-php-file-create-mkdir-fail)

**Blocking Direct IP Access**

Configuring sites-available & sites-enabled:

```
# mkdir /var/www/ip
# cd /etc/apache2/sites-available/
# vim 999-ip.conf
# a2ensite 999-ip.conf
# /etc/init.d/apache2 restart
```

`999-ip.conf`

```
<VirtualHost *:80>

	ServerName 

	Redirect 403 /

	DocumentRoot /var/www/ip

	ErrorLog /var/www/ip/error.log
	CustomLog /var/www/ip/access.log combined

</VirtualHost>
```

**Please check the link below for more information:**

* [Welcome to The Apache Software Foundation!](https://www.apache.org/)
* [Welcome! - The Apache HTTP Server Project](https://httpd.apache.org/)
* [Apache - Debian Wiki](https://wiki.debian.org/Apache)

## Mariadb

**Installing**

```
# apt install mariadb-server mariadb-client
```

**mysql_secure_installation**

```
# mysql_secure_installation
```

* [mysql_secure_installation](https://mariadb.com/kb/en/mariadb/mysql_secure_installation/)

**Configuration**

```
# mysql -u root -p -h localhost mysql

SELECT User, Host, plugin FROM user;

UPDATE user SET plugin='unix_socket' WHERE User='root';
UPDATE user SET plugin='' WHERE User='root';

FLUSH PRIVILEGES;

# /etc/init.d/mysql restart
```

* [Q1](https://stackoverflow.com/questions/39281594/error-1698-28000-access-denied-for-user-rootlocalhost)

**logging In**

To connect to MariaDB, type:

```
# mysql -u username -p -h localhost databasename
```

**Viewing**

Show the tables in the database:

```
show tables;
```

```
describe tablename;
```

```
select * from tablename;
```

**Inserting**

```
insert into books (Title, SeriesID, AuthorID)
values ("Lair of Bones", 2, 2);
```

**Modifying**

```
update books set Title = "The Hobbit" where BookID = 7;
```

**Deleteing**

```
delete from tablename where id=1;
```

**Please check the link below for more information:**

* [MariaDB.org - Supporting continuity and open collaboration](https://mariadb.org/)
* [MariaDB Knowledge Base](https://mariadb.com/kb/en/)
* [Teams/MySQL/MariaDB - Debian Wiki](https://wiki.debian.org/Teams/MySQL/MariaDB)

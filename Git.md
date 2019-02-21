# Hello, Git!

* [Git](https://git-scm.com/)
* [Git - Documentation](https://git-scm.com/doc)
* [Git - Book](https://git-scm.com/book/en/v2)

### Environment Configuration

Git comes with a tool called `git config` that lets you get and set configuration variables that control all aspects of how Git looks and operates.

**Getting Help**

```
$ git help config
```

**Checking Your Settings**

```
$ git config --list
$ git config user.name
```

**Your Identity**

```
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```

**SOCKS5**

```
$ git config --global http.proxy "socks5://127.0.0.1:0000"
$ git config --global https.proxy "socks5://127.0.0.1:0000"
$ git config --global http.proxy ""
$ git config --global https.proxy ""
```

### Basic Usage

**Initializing a Repository in an Existing Directory**

```
$ git init
```

**Cloning an Existing Repository**

```
$ git clone url projectName
```

**Showing Your Remotes**

```
$ git remote -v
```

**Adding Remote Repositories**

```
$ git remote add <shortname> <url>
$ git remote add pb https://github.com/paulboone/ticgit
```

**Fetching and Pulling from Your Remotes**

```
$ git fetch <remote>
$ git pull <remote>
```

**Pushing to Your Remotes**

```
$ git push <remote> <branch>
$ git push origin master
```

**Renaming and Removing Remotes**

```
$ git remote rename pb paul
$ git remote remove paul
```

**Getting All Branches**

```
$ git branch -av
```

**Creating a New Branch**

```
$ git branch testing
```

**Switching Branches**

```
$ git checkout testing
```

**create a new branch and switch to it at the same time**

```
$ git checkout -b testing
```

**Merging Branches**

```
$ git checkout master
$ git merge testing
```

**Deleting Branches**

```
$ git branch -d testing
```

**Checking the Status of Your Files**

```
$ git status
```

**Tracking The Files**

```
$ git add <file>...
```

**Staging Modified Files**

```
$ git add <file> ..
```

**Unstaging Files**

```
$ git reset HEAD <file>...
```

**discard changes in working directory**

```
$ git checkout -- <file>...
```

**Committing Your Changes**

```
$ git commit -a -m ""
```

**Viewing the Commit History**

```
$ git log
$ git log -p -2
$ git log --stat
$ git log --pretty=oneline
$ git log --pretty=format:"%h - %an, %ar : %s"
$ git log --pretty=format:"%h %s" --graph
$ git log --since=2.weeks
$ git log -Sfunction_name
```

**Removing Files**

```
$ git rm <file>...
```

**Moving Files**

```
$ git mv file_from file_to
```

**Listing Your Tags**

```
$ git tag
$ git tag -l "v1.8.5*"
```

**Creating Tags**

```
$ git tag -a v1.4 -m "my version 1.4"
```

**Showing Tags**

```
$ git show v1.4
```

**Sharing Tags**

```
$ git push origin --tags
$ git push origin v1.5
```

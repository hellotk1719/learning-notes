# Hello, Laravel!

* [Laravel - The PHP Framework For Web Artisans](https://laravel.com/)
* [Documentation 5.5 (LTS)](https://laravel.com/docs/5.5)

## Installation

### Server Requirements

* PHP >= 7.0.0
* OpenSSL PHP Extension
* PDO PHP Extension
* Mbstring PHP Extension
* Tokenizer PHP Extension
* XML PHP Extension

### Installing Laravel

```
composer create-project --prefer-dist laravel/laravel projectName "5.5.*"
```

**Please check the link below for more information:**

* [Installation - Laravel](https://laravel.com/docs/5.5/installation)
* [How to Setup a Laravel Project You Cloned from Github.com](https://devmarketer.io/learn/setup-laravel-project-cloned-github-com/)

## Configuration

### Timezone

**How to set timezone in Laravel?**

Please open the file `/config/app.php`. Go down the page and check **Application Timezone** where you will find

```php
'timezone' => 'UTC',
```

Here you can add your timezone like

```php
'timezone' => 'Asia/Shanghai',
```

If you want to manage your timezone from `.env` file, then you can change below code in your `/config/app.php` file.

```php
'timezone' => env('APP_TIMEZONE', 'UTC'),
```

and add the below line in your `.env` file.

```
APP_TIMEZONE=Asia/Shanghai
```

**Please check the link below for more information:**

* [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time)
* [Configuration - Laravel](https://laravel.com/docs/5.5/configuration)
* [List of Supported Timezones](http://php.net/manual/en/timezones.php)

### Localization

**Installing Laravel-lang**

```
composer require caouecs/laravel-lang:~3.0
```

Files of languages are in `/vendor/caouecs/laravel-lang/src` directory.

Copy the folders of languages that you want, in the `/resources/lang` folder of your Laravel application.

**Usage [Laravel only]**

In the file `/config/app.php`, change the value of `locale` by the short name of your language.

**Please check the link below for more information:**

* [Localization - Laravel](https://laravel.com/docs/5.5/localization)
* [Laravel-lang](https://github.com/caouecs/Laravel-lang)

### Database

The database configuration for your application is located at `/config/database.php`.

By default, `.env` is short for environment and thus that is your environment configurations.

**Read & Write Connections**

In the `.env` file fill in the `DB_CONNECTION`, `DB_HOST`, `DB_PORT`, `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD` options to match the credentials of the database you just created.

**Please check the link below for more information:**

* [Database: Getting Started - Laravel](https://laravel.com/docs/5.5/database)

**Modifying the engine of MySQL**

Open the file `/config/database.php`. Go down the page and check `'mysql' => [],` where you will find

```php
'mysql' => [
    'driver' => 'mysql',
    'host' => env('DB_HOST', '127.0.0.1'),
    'port' => env('DB_PORT', '3306'),
    'database' => env('DB_DATABASE', 'forge'),
    'username' => env('DB_USERNAME', 'forge'),
    'password' => env('DB_PASSWORD', ''),
    'unix_socket' => env('DB_SOCKET', ''),
    'charset' => 'utf8mb4',
    'collation' => 'utf8mb4_unicode_ci',
    'prefix' => '',
    'strict' => true,
    'engine' => null,
],
```

Here you can add your engine like

```php
'mysql' => [
    ......
    'engine' => 'InnoDB',
],
```

**Please check the link below for more information:**

* [Database: Migrations - Laravel](https://laravel.com/docs/5.5/migrations#tables)
* [mysql - Laravel Migration Error: Syntax error or access violation: 1071 Specified key was too long;](https://stackoverflow.com/questions/42244541/laravel-migration-error-syntax-error-or-access-violation-1071-specified-key-wa)

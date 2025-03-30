# Installation

- [Meet Laravel](#meet-laravel)
    - [Why Laravel?](#why-laravel)
- [Creating a Laravel Application](#creating-a-laravel-project)
    - [Installing PHP and the Laravel Installer](#installing-php)
    - [Creating an Application](#creating-an-application)
- [Initial Configuration](#initial-configuration)
    - [Environment Based Configuration](#environment-based-configuration)
    - [Databases and Migrations](#databases-and-migrations)
    - [Directory Configuration](#directory-configuration)
- [Installation Using Herd](#installation-using-herd)
    - [Herd on macOS](#herd-on-macos)
    - [Herd on Windows](#herd-on-windows)
- [IDE Support](#ide-support)
- [Next Steps](#next-steps)
    - [Laravel the Full Stack Framework](#laravel-the-fullstack-framework)
    - [Laravel the API Backend](#laravel-the-api-backend)

<div style="page-break-after: always"></div>

<a name="meet-laravel"></a>
## Meet Laravel

Laravel is a web application framework with expressive, elegant syntax. A web framework provides a structure and starting point for creating your application, allowing you to focus on creating something amazing while we sweat the details.

Laravel strives to provide an amazing developer experience while providing powerful features such as thorough dependency injection, an expressive database abstraction layer, queues and scheduled jobs, unit and integration testing, and more.

Whether you are new to PHP web frameworks or have years of experience, Laravel is a framework that can grow with you. We'll help you take your first steps as a web developer or give you a boost as you take your expertise to the next level. We can't wait to see what you build.

<a name="why-laravel"></a>
### Why Laravel?

There are a variety of tools and frameworks available to you when building a web application. However, we believe Laravel is the best choice for building modern, full-stack web applications.

#### A Progressive Framework

We like to call Laravel a "progressive" framework. By that, we mean that Laravel grows with you. If you're just taking your first steps into web development, Laravel's vast library of documentation, guides, and [video tutorials](https://laracasts.com) will help you learn the ropes without becoming overwhelmed.

If you're a senior developer, Laravel gives you robust tools for [dependency injection](/docs/{{version}}/container), [unit testing](/docs/{{version}}/testing), [queues](/docs/{{version}}/queues), [real-time events](/docs/{{version}}/broadcasting), and more. Laravel is fine-tuned for building professional web applications and ready to handle enterprise work loads.

#### A Scalable Framework

Laravel is incredibly scalable. Thanks to the scaling-friendly nature of PHP and Laravel's built-in support for fast, distributed cache systems like Redis, horizontal scaling with Laravel is a breeze. In fact, Laravel applications have been easily scaled to handle hundreds of millions of requests per month.

Need extreme scaling? Platforms like [Laravel Cloud](https://cloud.laravel.com) allow you to run your Laravel application at nearly limitless scale.

#### A Community Framework

Laravel combines the best packages in the PHP ecosystem to offer the most robust and developer friendly framework available. In addition, thousands of talented developers from around the world have [contributed to the framework](https://github.com/laravel/framework). Who knows, maybe you'll even become a Laravel contributor.

<div style="page-break-after: always"></div>

<a name="creating-a-laravel-project"></a>
## Creating a Laravel Application

<a name="installing-php"></a>
### Installing PHP and the Laravel Installer

Before creating your first Laravel application, make sure that your local machine has [PHP](https://php.net), [Composer](https://getcomposer.org), and [the Laravel installer](https://github.com/laravel/installer) installed. In addition, you should install either [Node and NPM](https://nodejs.org) or [Bun](https://bun.sh/) so that you can compile your application's frontend assets.

If you don't have PHP and Composer installed on your local machine, the following commands will install PHP, Composer, and the Laravel installer on macOS, Windows, or Linux:

```shell tab=macOS
/bin/bash -c "$(curl -fsSL https://php.new/install/mac/8.4)"
```

```shell tab=Windows PowerShell
# Run as administrator...
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://php.new/install/windows/8.4'))
```

```shell tab=Linux
/bin/bash -c "$(curl -fsSL https://php.new/install/linux/8.4)"
```

After running one of the commands above, you should restart your terminal session. To update PHP, Composer, and the Laravel installer after installing them via `php.new`, you can re-run the command in your terminal.

If you already have PHP and Composer installed, you may install the Laravel installer via Composer:

```shell
composer global require laravel/installer
```

> [!NOTE]
> For a fully-featured, graphical PHP installation and management experience, check out [Laravel Herd](#installation-using-herd).

<div style="page-break-after: always"></div>

<a name="creating-an-application"></a>
### Creating an Application

After you have installed PHP, Composer, and the Laravel installer, you're ready to create a new Laravel application. The Laravel installer will prompt you to select your preferred testing framework, database, and starter kit:

```shell
laravel new example-app
```

Once the application has been created, you can start Laravel's local development server, queue worker, and Vite development server using the `dev` Composer script:

```shell
cd example-app
npm install && npm run build
composer run dev
```

Once you have started the development server, your application will be accessible in your web browser at [http://localhost:8000](http://localhost:8000). Next, you're ready to [start taking your next steps into the Laravel ecosystem](#next-steps). Of course, you may also want to [configure a database](#databases-and-migrations).

> [!NOTE]
> If you would like a head start when developing your Laravel application, consider using one of our [starter kits](/docs/{{version}}/starter-kits). Laravel's starter kits provide backend and frontend authentication scaffolding for your new Laravel application.

<a name="initial-configuration"></a>
## Initial Configuration

All of the configuration files for the Laravel framework are stored in the `config` directory. Each option is documented, so feel free to look through the files and get familiar with the options available to you.

Laravel needs almost no additional configuration out of the box. You are free to get started developing! However, you may wish to review the `config/app.php` file and its documentation. It contains several options such as `url` and `locale` that you may wish to change according to your application.

<a name="environment-based-configuration"></a>
### Environment Based Configuration

Since many of Laravel's configuration option values may vary depending on whether your application is running on your local machine or on a production web server, many important configuration values are defined using the `.env` file that exists at the root of your application.

Your `.env` file should not be committed to your application's source control, since each developer / server using your application could require a different environment configuration. Furthermore, this would be a security risk in the event an intruder gains access to your source control repository, since any sensitive credentials would be exposed.

> [!NOTE]
> For more information about the `.env` file and environment based configuration, check out the full [configuration documentation](/docs/{{version}}/configuration#environment-configuration).

<div style="page-break-after: always"></div>

<a name="databases-and-migrations"></a>
### Databases and Migrations

Now that you have created your Laravel application, you probably want to store some data in a database. By default, your application's `.env` configuration file specifies that Laravel will be interacting with an SQLite database.

During the creation of the application, Laravel created a `database/database.sqlite` file for you, and ran the necessary migrations to create the application's database tables.

If you prefer to use another database driver such as MySQL or PostgreSQL, you can update your `.env` configuration file to use the appropriate database. For example, if you wish to use MySQL, update your `.env` configuration file's `DB_*` variables like so:

```ini
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=
```

If you choose to use a database other than SQLite, you will need to create the database and run your application's [database migrations](/docs/{{version}}/migrations):

```shell
php artisan migrate
```

> [!NOTE]
> If you are developing on macOS or Windows and need to install MySQL, PostgreSQL, or Redis locally, consider using [Herd Pro](https://herd.laravel.com/#plans) or [DBngin](https://dbngin.com/).

<a name="directory-configuration"></a>
### Directory Configuration

Laravel should always be served out of the root of the "web directory" configured for your web server. You should not attempt to serve a Laravel application out of a subdirectory of the "web directory". Attempting to do so could expose sensitive files present within your application.

<div style="page-break-after: always"></div>

<a name="installation-using-herd"></a>
## Installation Using Herd

[Laravel Herd](https://herd.laravel.com) is a blazing fast, native Laravel and PHP development environment for macOS and Windows. Herd includes everything you need to get started with Laravel development, including PHP and Nginx.

Once you install Herd, you're ready to start developing with Laravel. Herd includes command line tools for `php`, `composer`, `laravel`, `expose`, `node`, `npm`, and `nvm`.

> [!NOTE]
> [Herd Pro](https://herd.laravel.com/#plans) augments Herd with additional powerful features, such as the ability to create and manage local MySQL, Postgres, and Redis databases, as well as local mail viewing and log monitoring.

<a name="herd-on-macos"></a>
### Herd on macOS

If you develop on macOS, you can download the Herd installer from the [Herd website](https://herd.laravel.com). The installer automatically downloads the latest version of PHP and configures your Mac to always run [Nginx](https://www.nginx.com/) in the background.

Herd for macOS uses [dnsmasq](https://en.wikipedia.org/wiki/Dnsmasq) to support "parked" directories. Any Laravel application in a parked directory will automatically be served by Herd. By default, Herd creates a parked directory at `~/Herd` and you can access any Laravel application in this directory on the `.test` domain using its directory name.

After installing Herd, the fastest way to create a new Laravel application is using the Laravel CLI, which is bundled with Herd:

```shell
cd ~/Herd
laravel new my-app
cd my-app
herd open
```

Of course, you can always manage your parked directories and other PHP settings via Herd's UI, which can be opened from the Herd menu in your system tray.

You can learn more about Herd by checking out the [Herd documentation](https://herd.laravel.com/docs).

<div style="page-break-after: always"></div>

<a name="herd-on-windows"></a>
### Herd on Windows

You can download the Windows installer for Herd on the [Herd website](https://herd.laravel.com/windows). After the installation finishes, you can start Herd to complete the onboarding process and access the Herd UI for the first time.

The Herd UI is accessible by left-clicking on Herd's system tray icon. A right-click opens the quick menu with access to all tools that you need on a daily basis.

During installation, Herd creates a "parked" directory in your home directory at `%USERPROFILE%\Herd`. Any Laravel application in a parked directory will automatically be served by Herd, and you can access any Laravel application in this directory on the `.test` domain using its directory name.

After installing Herd, the fastest way to create a new Laravel application is using the Laravel CLI, which is bundled with Herd. To get started, open Powershell and run the following commands:

```shell
cd ~\Herd
laravel new my-app
cd my-app
herd open
```

You can learn more about Herd by checking out the [Herd documentation for Windows](https://herd.laravel.com/docs/windows).

<a name="ide-support"></a>
## IDE Support

You are free to use any code editor you wish when developing Laravel applications; however, [PhpStorm](https://www.jetbrains.com/phpstorm/laravel/) offers extensive support for Laravel and its ecosystem, including [Laravel Pint](https://www.jetbrains.com/help/phpstorm/using-laravel-pint.html).

In addition, the community maintained [Laravel Idea](https://laravel-idea.com/) PhpStorm plugin offers a variety of helpful IDE augmentations, including code generation, Eloquent syntax completion, validation rule completion, and more.

If you develop in [Visual Studio Code (VS Code)](https://code.visualstudio.com), the official [Laravel VS Code Extension](https://marketplace.visualstudio.com/items?itemName=laravel.vscode-laravel) is now available. This extension brings Laravel-specific tools directly into your VS Code environment, enhancing productivity.

<div style="page-break-after: always"></div>

<a name="next-steps"></a>
## Next Steps

Now that you have created your Laravel application, you may be wondering what to learn next. First, we strongly recommend becoming familiar with how Laravel works by reading the following documentation:

<div class="content-list" markdown="1">

- [Request Lifecycle](/docs/{{version}}/lifecycle)
- [Configuration](/docs/{{version}}/configuration)
- [Directory Structure](/docs/{{version}}/structure)
- [Frontend](/docs/{{version}}/frontend)
- [Service Container](/docs/{{version}}/container)
- [Facades](/docs/{{version}}/facades)

</div>

How you want to use Laravel will also dictate the next steps on your journey. There are a variety of ways to use Laravel, and we'll explore two primary use cases for the framework below.

<a name="laravel-the-fullstack-framework"></a>
### Laravel the Full Stack Framework

Laravel may serve as a full stack framework. By "full stack" framework we mean that you are going to use Laravel to route requests to your application and render your frontend via [Blade templates](/docs/{{version}}/blade) or a single-page application hybrid technology like [Inertia](https://inertiajs.com). This is the most common way to use the Laravel framework, and, in our opinion, the most productive way to use Laravel.

If this is how you plan to use Laravel, you may want to check out our documentation on [frontend development](/docs/{{version}}/frontend), [routing](/docs/{{version}}/routing), [views](/docs/{{version}}/views), or the [Eloquent ORM](/docs/{{version}}/eloquent). In addition, you might be interested in learning about community packages like [Livewire](https://livewire.laravel.com) and [Inertia](https://inertiajs.com). These packages allow you to use Laravel as a full-stack framework while enjoying many of the UI benefits provided by single-page JavaScript applications.

If you are using Laravel as a full stack framework, we also strongly encourage you to learn how to compile your application's CSS and JavaScript using [Vite](/docs/{{version}}/vite).

> [!NOTE]
> If you want to get a head start building your application, check out one of our official [application starter kits](/docs/{{version}}/starter-kits).

<a name="laravel-the-api-backend"></a>
### Laravel the API Backend

Laravel may also serve as an API backend to a JavaScript single-page application or mobile application. For example, you might use Laravel as an API backend for your [Next.js](https://nextjs.org) application. In this context, you may use Laravel to provide [authentication](/docs/{{version}}/sanctum) and data storage / retrieval for your application, while also taking advantage of Laravel's powerful services such as queues, emails, notifications, and more.

If this is how you plan to use Laravel, you may want to check out our documentation on [routing](/docs/{{version}}/routing), [Laravel Sanctum](/docs/{{version}}/sanctum), and the [Eloquent ORM](/docs/{{version}}/eloquent).

<div style="page-break-after: always"></div>


# Configuration

- [Introduction](#introduction)
- [Environment Configuration](#environment-configuration)
    - [Environment Variable Types](#environment-variable-types)
    - [Retrieving Environment Configuration](#retrieving-environment-configuration)
    - [Determining the Current Environment](#determining-the-current-environment)
    - [Encrypting Environment Files](#encrypting-environment-files)
- [Accessing Configuration Values](#accessing-configuration-values)
- [Configuration Caching](#configuration-caching)
- [Configuration Publishing](#configuration-publishing)
- [Debug Mode](#debug-mode)
- [Maintenance Mode](#maintenance-mode)

<a name="introduction"></a>
## Introduction

All of the configuration files for the Laravel framework are stored in the `config` directory. Each option is documented, so feel free to look through the files and get familiar with the options available to you.

These configuration files allow you to configure things like your database connection information, your mail server information, as well as various other core configuration values such as your application URL and encryption key.

<a name="the-about-command"></a>
#### The `about` Command

Laravel can display an overview of your application's configuration, drivers, and environment via the `about` Artisan command.

```shell
php artisan about
```

If you're only interested in a particular section of the application overview output, you may filter for that section using the `--only` option:

```shell
php artisan about --only=environment
```

Or, to explore a specific configuration file's values in detail, you may use the `config:show` Artisan command:

```shell
php artisan config:show database
```
<div style="page-break-after: always"></div>

<a name="environment-configuration"></a>
## Environment Configuration

It is often helpful to have different configuration values based on the environment where the application is running. For example, you may wish to use a different cache driver locally than you do on your production server.

To make this a cinch, Laravel utilizes the [DotEnv](https://github.com/vlucas/phpdotenv) PHP library. In a fresh Laravel installation, the root directory of your application will contain a `.env.example` file that defines many common environment variables. During the Laravel installation process, this file will automatically be copied to `.env`.

Laravel's default `.env` file contains some common configuration values that may differ based on whether your application is running locally or on a production web server. These values are then read by the configuration files within the `config` directory using Laravel's `env` function.

If you are developing with a team, you may wish to continue including and updating the `.env.example` file with your application. By putting placeholder values in the example configuration file, other developers on your team can clearly see which environment variables are needed to run your application.

> [!NOTE]
> Any variable in your `.env` file can be overridden by external environment variables such as server-level or system-level environment variables.

<a name="environment-file-security"></a>
#### Environment File Security

Your `.env` file should not be committed to your application's source control, since each developer / server using your application could require a different environment configuration. Furthermore, this would be a security risk in the event an intruder gains access to your source control repository, since any sensitive credentials would get exposed.

However, it is possible to encrypt your environment file using Laravel's built-in [environment encryption](#encrypting-environment-files). Encrypted environment files may be placed in source control safely.

<a name="additional-environment-files"></a>
#### Additional Environment Files

Before loading your application's environment variables, Laravel determines if an `APP_ENV` environment variable has been externally provided or if the `--env` CLI argument has been specified. If so, Laravel will attempt to load an `.env.[APP_ENV]` file if it exists. If it does not exist, the default `.env` file will be loaded.

<div style="page-break-after: always"></div>

<a name="environment-variable-types"></a>
### Environment Variable Types

All variables in your `.env` files are typically parsed as strings, so some reserved values have been created to allow you to return a wider range of types from the `env()` function:

<div class="overflow-auto">

| `.env` Value | `env()` Value |
| ------------ | ------------- |
| true         | (bool) true   |
| (true)       | (bool) true   |
| false        | (bool) false  |
| (false)      | (bool) false  |
| empty        | (string) ''   |
| (empty)      | (string) ''   |
| null         | (null) null   |
| (null)       | (null) null   |

</div>

If you need to define an environment variable with a value that contains spaces, you may do so by enclosing the value in double quotes:

```ini
APP_NAME="My Application"
```

<a name="retrieving-environment-configuration"></a>
### Retrieving Environment Configuration

All of the variables listed in the `.env` file will be loaded into the `$_ENV` PHP super-global when your application receives a request. However, you may use the `env` function to retrieve values from these variables in your configuration files. In fact, if you review the Laravel configuration files, you will notice many of the options are already using this function:

```php
'debug' => env('APP_DEBUG', false),
```

The second value passed to the `env` function is the "default value". This value will be returned if no environment variable exists for the given key.

<a name="determining-the-current-environment"></a>
### Determining the Current Environment

The current application environment is determined via the `APP_ENV` variable from your `.env` file. You may access this value via the `environment` method on the `App` [facade](/docs/{{version}}/facades):

```php
use Illuminate\Support\Facades\App;
$environment = App::environment();
```
<div style="page-break-after: always"></div>

You may also pass arguments to the `environment` method to determine if the environment matches a given value. The method will return `true` if the environment matches any of the given values:

```php
if (App::environment('local')) {
    // The environment is local
}

if (App::environment(['local', 'staging'])) {
    // The environment is either local OR staging...
}
```

> [!NOTE]
> The current application environment detection can be overridden by defining a server-level `APP_ENV` environment variable.

<a name="encrypting-environment-files"></a>
### Encrypting Environment Files

Unencrypted environment files should never be stored in source control. However, Laravel allows you to encrypt your environment files so that they may safely be added to source control with the rest of your application.

<a name="encryption"></a>
#### Encryption

To encrypt an environment file, you may use the `env:encrypt` command:

```shell
php artisan env:encrypt
```

Running the `env:encrypt` command will encrypt your `.env` file and place the encrypted contents in an `.env.encrypted` file. The decryption key is presented in the output of the command and should be stored in a secure password manager. If you would like to provide your own encryption key you may use the `--key` option when invoking the command:

```shell
php artisan env:encrypt --key=3UVsEgGVK36XN82KKeyLFMhvosbZN1aF
```

> [!NOTE]
> The length of the key provided should match the key length required by the encryption cipher being used. By default, Laravel will use the `AES-256-CBC` cipher which requires a 32 character key. You are free to use any cipher supported by Laravel's [encrypter](/docs/{{version}}/encryption) by passing the `--cipher` option when invoking the command.

If your application has multiple environment files, such as `.env` and `.env.staging`, you may specify the environment file that should be encrypted by providing the environment name via the `--env` option:

```shell
php artisan env:encrypt --env=staging
```

<div style="page-break-after: always"></div>

<a name="decryption"></a>
#### Decryption

To decrypt an environment file, you may use the `env:decrypt` command. This command requires a decryption key, which Laravel will retrieve from the `LARAVEL_ENV_ENCRYPTION_KEY` environment variable:

```shell
php artisan env:decrypt
```

Or, the key may be provided directly to the command via the `--key` option:

```shell
php artisan env:decrypt --key=3UVsEgGVK36XN82KKeyLFMhvosbZN1aF
```

When the `env:decrypt` command is invoked, Laravel will decrypt the contents of the `.env.encrypted` file and place the decrypted contents in the `.env` file.

The `--cipher` option may be provided to the `env:decrypt` command in order to use a custom encryption cipher:

```shell
php artisan env:decrypt --key=qUWuNRdfuImXcKxZ --cipher=AES-128-CBC
```

If your application has multiple environment files, such as `.env` and `.env.staging`, you may specify the environment file that should be decrypted by providing the environment name via the `--env` option:

```shell
php artisan env:decrypt --env=staging
```

In order to overwrite an existing environment file, you may provide the `--force` option to the `env:decrypt` command:

```shell
php artisan env:decrypt --force
```

<div style="page-break-after: always"></div>

<a name="accessing-configuration-values"></a>
## Accessing Configuration Values

You may easily access your configuration values using the `Config` facade or global `config` function from anywhere in your application. The configuration values may be accessed using "dot" syntax, which includes the name of the file and option you wish to access. A default value may also be specified and will be returned if the configuration option does not exist:

```php
use Illuminate\Support\Facades\Config;

$value = Config::get('app.timezone');

$value = config('app.timezone');

// Retrieve a default value if the configuration value does not exist...
$value = config('app.timezone', 'Asia/Seoul');
```

To set configuration values at runtime, you may invoke the `Config` facade's `set` method or pass an array to the `config` function:

```php
Config::set('app.timezone', 'America/Chicago');

config(['app.timezone' => 'America/Chicago']);
```

To assist with static analysis, the `Config` facade also provides typed configuration retrieval methods. If the retrieved configuration value does not match the expected type, an exception will be thrown:

```php
Config::string('config-key');
Config::integer('config-key');
Config::float('config-key');
Config::boolean('config-key');
Config::array('config-key');
```
<div style="page-break-after: always"></div>

<a name="configuration-caching"></a>
## Configuration Caching

To give your application a speed boost, you should cache all of your configuration files into a single file using the `config:cache` Artisan command. This will combine all of the configuration options for your application into a single file which can be quickly loaded by the framework.

You should typically run the `php artisan config:cache` command as part of your production deployment process. The command should not be run during local development as configuration options will frequently need to be changed during the course of your application's development.

Once the configuration has been cached, your application's `.env` file will not be loaded by the framework during requests or Artisan commands; therefore, the `env` function will only return external, system level environment variables.

For this reason, you should ensure you are only calling the `env` function from within your application's configuration (`config`) files. You can see many examples of this by examining Laravel's default configuration files. Configuration values may be accessed from anywhere in your application using the `config` function [described above](#accessing-configuration-values).

The `config:clear` command may be used to purge the cached configuration:

```shell
php artisan config:clear
```

> [!WARNING]
> If you execute the `config:cache` command during your deployment process, you should be sure that you are only calling the `env` function from within your configuration files. Once the configuration has been cached, the `.env` file will not be loaded; therefore, the `env` function will only return external, system level environment variables.

<a name="configuration-publishing"></a>
## Configuration Publishing

Most of Laravel's configuration files are already published in your application's `config` directory; however, certain configuration files like `cors.php` and `view.php` are not published by default, as most applications will never need to modify them.

However, you may use the `config:publish` Artisan command to publish any configuration files that are not published by default:

```shell
php artisan config:publish

php artisan config:publish --all
```
<div style="page-break-after: always"></div>

<a name="debug-mode"></a>
## Debug Mode

The `debug` option in your `config/app.php` configuration file determines how much information about an error is actually displayed to the user. By default, this option is set to respect the value of the `APP_DEBUG` environment variable, which is stored in your `.env` file.

> [!WARNING]
> For local development, you should set the `APP_DEBUG` environment variable to `true`. **In your production environment, this value should always be `false`. If the variable is set to `true` in production, you risk exposing sensitive configuration values to your application's end users.**

<a name="maintenance-mode"></a>
## Maintenance Mode

When your application is in maintenance mode, a custom view will be displayed for all requests into your application. This makes it easy to "disable" your application while it is updating or when you are performing maintenance. A maintenance mode check is included in the default middleware stack for your application. If the application is in maintenance mode, a `Symfony\Component\HttpKernel\Exception\HttpException` instance will be thrown with a status code of 503.

To enable maintenance mode, execute the `down` Artisan command:

```shell
php artisan down
```

If you would like the `Refresh` HTTP header to be sent with all maintenance mode responses, you may provide the `refresh` option when invoking the `down` command. The `Refresh` header will instruct the browser to automatically refresh the page after the specified number of seconds:

```shell
php artisan down --refresh=15
```

You may also provide a `retry` option to the `down` command, which will be set as the `Retry-After` HTTP header's value, although browsers generally ignore this header:

```shell
php artisan down --retry=60
```

<div style="page-break-after: always"></div>

<a name="bypassing-maintenance-mode"></a>
#### Bypassing Maintenance Mode

To allow maintenance mode to be bypassed using a secret token, you may use the `secret` option to specify a maintenance mode bypass token:

```shell
php artisan down --secret="1630542a-246b-4b66-afa1-dd72a4c43515"
```

After placing the application in maintenance mode, you may navigate to the application URL matching this token and Laravel will issue a maintenance mode bypass cookie to your browser:

```shell
https://example.com/1630542a-246b-4b66-afa1-dd72a4c43515
```

If you would like Laravel to generate the secret token for you, you may use the `with-secret` option. The secret will be displayed to you once the application is in maintenance mode:

```shell
php artisan down --with-secret
```

When accessing this hidden route, you will then be redirected to the `/` route of the application. Once the cookie has been issued to your browser, you will be able to browse the application normally as if it was not in maintenance mode.

> [!NOTE]
> Your maintenance mode secret should typically consist of alpha-numeric characters and, optionally, dashes. You should avoid using characters that have special meaning in URLs such as `?` or `&`.

<a name="maintenance-mode-on-multiple-servers"></a>
#### Maintenance Mode on Multiple Servers

By default, Laravel determines if your application is in maintenance mode using a file-based system. This means to activate maintenance mode, the `php artisan down` command has to be executed on each server hosting your application.

Alternatively, Laravel offers a cache-based method for handling maintenance mode. This method requires running the `php artisan down` command on just one server. To use this approach, modify the maintenance mode variables in your application's `.env` file. You should select a cache `store` that is accessible by all of your servers. This ensures the maintenance mode status is consistently maintained across every server:

```ini
APP_MAINTENANCE_DRIVER=cache
APP_MAINTENANCE_STORE=database
```

<div style="page-break-after: always"></div>

<a name="pre-rendering-the-maintenance-mode-view"></a>
#### Pre-Rendering the Maintenance Mode View

If you utilize the `php artisan down` command during deployment, your users may still occasionally encounter errors if they access the application while your Composer dependencies or other infrastructure components are updating. This occurs because a significant part of the Laravel framework must boot in order to determine your application is in maintenance mode and render the maintenance mode view using the templating engine.

For this reason, Laravel allows you to pre-render a maintenance mode view that will be returned at the very beginning of the request cycle. This view is rendered before any of your application's dependencies have loaded. You may pre-render a template of your choice using the `down` command's `render` option:

```shell
php artisan down --render="errors::503"
```

<a name="redirecting-maintenance-mode-requests"></a>
#### Redirecting Maintenance Mode Requests

While in maintenance mode, Laravel will display the maintenance mode view for all application URLs the user attempts to access. If you wish, you may instruct Laravel to redirect all requests to a specific URL. This may be accomplished using the `redirect` option. For example, you may wish to redirect all requests to the `/` URI:

```shell
php artisan down --redirect=/
```

<a name="disabling-maintenance-mode"></a>
#### Disabling Maintenance Mode

To disable maintenance mode, use the `up` command:

```shell
php artisan up
```

> [!NOTE]
> You may customize the default maintenance mode template by defining your own template at `resources/views/errors/503.blade.php`.

<a name="maintenance-mode-queues"></a>
#### Maintenance Mode and Queues

While your application is in maintenance mode, no [queued jobs](/docs/{{version}}/queues) will be handled. The jobs will continue to be handled as normal once the application is out of maintenance mode.

<a name="alternatives-to-maintenance-mode"></a>
#### Alternatives to Maintenance Mode

Since maintenance mode requires your application to have several seconds of downtime, consider running your applications on a fully-managed platform like [Laravel Cloud](https://cloud.laravel.com) to accomplish zero-downtime deployment with Laravel.

<div style="page-break-after: always"></div>


# Directory Structure

- [Introduction](#introduction)
- [The Root Directory](#the-root-directory)
    - [The `app` Directory](#the-root-app-directory)
    - [The `bootstrap` Directory](#the-bootstrap-directory)
    - [The `config` Directory](#the-config-directory)
    - [The `database` Directory](#the-database-directory)
    - [The `public` Directory](#the-public-directory)
    - [The `resources` Directory](#the-resources-directory)
    - [The `routes` Directory](#the-routes-directory)
    - [The `storage` Directory](#the-storage-directory)
    - [The `tests` Directory](#the-tests-directory)
    - [The `vendor` Directory](#the-vendor-directory)
- [The App Directory](#the-app-directory)
    - [The `Broadcasting` Directory](#the-broadcasting-directory)
    - [The `Console` Directory](#the-console-directory)
    - [The `Events` Directory](#the-events-directory)
    - [The `Exceptions` Directory](#the-exceptions-directory)
    - [The `Http` Directory](#the-http-directory)
    - [The `Jobs` Directory](#the-jobs-directory)
    - [The `Listeners` Directory](#the-listeners-directory)
    - [The `Mail` Directory](#the-mail-directory)
    - [The `Models` Directory](#the-models-directory)
    - [The `Notifications` Directory](#the-notifications-directory)
    - [The `Policies` Directory](#the-policies-directory)
    - [The `Providers` Directory](#the-providers-directory)
    - [The `Rules` Directory](#the-rules-directory)

<div style="page-break-after: always"></div>

<a name="introduction"></a>
## Introduction

The default Laravel application structure is intended to provide a great starting point for both large and small applications. But you are free to organize your application however you like. Laravel imposes almost no restrictions on where any given class is located - as long as Composer can autoload the class.

<a name="the-root-directory"></a>
## The Root Directory

<a name="the-root-app-directory"></a>
### The App Directory

The `app` directory contains the core code of your application. We'll explore this directory in more detail soon; however, almost all of the classes in your application will be in this directory.

<a name="the-bootstrap-directory"></a>
### The Bootstrap Directory

The `bootstrap` directory contains the `app.php` file which bootstraps the framework. This directory also houses a `cache` directory which contains framework generated files for performance optimization such as the route and services cache files.

<a name="the-config-directory"></a>
### The Config Directory

The `config` directory, as the name implies, contains all of your application's configuration files. It's a great idea to read through all of these files and familiarize yourself with all of the options available to you.

<a name="the-database-directory"></a>
### The Database Directory

The `database` directory contains your database migrations, model factories, and seeds. If you wish, you may also use this directory to hold an SQLite database.

<a name="the-public-directory"></a>
### The Public Directory

The `public` directory contains the `index.php` file, which is the entry point for all requests entering your application and configures autoloading. This directory also houses your assets such as images, JavaScript, and CSS.

<a name="the-resources-directory"></a>
### The Resources Directory

The `resources` directory contains your [views](/docs/{{version}}/views) as well as your raw, un-compiled assets such as CSS or JavaScript.

<div style="page-break-after: always"></div>

<a name="the-routes-directory"></a>
### The Routes Directory

The `routes` directory contains all of the route definitions for your application. By default, two route files are included with Laravel: `web.php` and `console.php`.

The `web.php` file contains routes that Laravel places in the `web` middleware group, which provides session state, CSRF protection, and cookie encryption. If your application does not offer a stateless, RESTful API then all your routes will most likely be defined in the `web.php` file.

The `console.php` file is where you may define all of your closure based console commands. Each closure is bound to a command instance allowing a simple approach to interacting with each command's IO methods. Even though this file does not define HTTP routes, it defines console based entry points (routes) into your application. You may also [schedule](/docs/{{version}}/scheduling) tasks in the `console.php` file.

Optionally, you may install additional route files for API routes (`api.php`) and broadcasting channels (`channels.php`), via the `install:api` and `install:broadcasting` Artisan commands.

The `api.php` file contains routes that are intended to be stateless, so requests entering the application through these routes are intended to be authenticated [via tokens](/docs/{{version}}/sanctum) and will not have access to session state.

The `channels.php` file is where you may register all of the [event broadcasting](/docs/{{version}}/broadcasting) channels that your application supports.

<a name="the-storage-directory"></a>
### The Storage Directory

The `storage` directory contains your logs, compiled Blade templates, file based sessions, file caches, and other files generated by the framework. This directory is segregated into `app`, `framework`, and `logs` directories. The `app` directory may be used to store any files generated by your application. The `framework` directory is used to store framework generated files and caches. Finally, the `logs` directory contains your application's log files.

The `storage/app/public` directory may be used to store user-generated files, such as profile avatars, that should be publicly accessible. You should create a symbolic link at `public/storage` which points to this directory. You may create the link using the `php artisan storage:link` Artisan command.

<a name="the-tests-directory"></a>
### The Tests Directory

The `tests` directory contains your automated tests. Example [Pest](https://pestphp.com) or [PHPUnit](https://phpunit.de/) unit tests and feature tests are provided out of the box. Each test class should be suffixed with the word `Test`. You may run your tests using the `/vendor/bin/pest` or `/vendor/bin/phpunit` commands. Or, if you would like a more detailed and beautiful representation of your test results, you may run your tests using the `php artisan test` Artisan command.

<a name="the-vendor-directory"></a>
### The Vendor Directory

The `vendor` directory contains your [Composer](https://getcomposer.org) dependencies.

<div style="page-break-after: always"></div>

<a name="the-app-directory"></a>
## The App Directory

The majority of your application is housed in the `app` directory. By default, this directory is namespaced under `App` and is autoloaded by Composer using the [PSR-4 autoloading standard](https://www.php-fig.org/psr/psr-4/).

By default, the `app` directory contains the `Http`, `Models`, and `Providers` directories. However, over time, a variety of other directories will be generated inside the app directory as you use the make Artisan commands to generate classes. For example, the `app/Console` directory will not exist until you execute the `make:command` Artisan command to generate a command class.

Both the `Console` and `Http` directories are further explained in their respective sections below, but think of the `Console` and `Http` directories as providing an API into the core of your application. The HTTP protocol and CLI are both mechanisms to interact with your application, but do not actually contain application logic. In other words, they are two ways of issuing commands to your application. The `Console` directory contains all of your Artisan commands, while the `Http` directory contains your controllers, middleware, and requests.

> [!NOTE]
> Many of the classes in the `app` directory can be generated by Artisan via commands. To review the available commands, run the `php artisan list make` command in your terminal.

<a name="the-broadcasting-directory"></a>
### The Broadcasting Directory

The `Broadcasting` directory contains all of the broadcast channel classes for your application. These classes are generated using the `make:channel` command. This directory does not exist by default, but will be created for you when you create your first channel. To learn more about channels, check out the documentation on [event broadcasting](/docs/{{version}}/broadcasting).

<a name="the-console-directory"></a>
### The Console Directory

The `Console` directory contains all of the custom Artisan commands for your application. These commands may be generated using the `make:command` command.

<a name="the-events-directory"></a>
### The Events Directory

This directory does not exist by default, but will be created for you by the `event:generate` and `make:event` Artisan commands. The `Events` directory houses [event classes](/docs/{{version}}/events). Events may be used to alert other parts of your application that a given action has occurred, providing a great deal of flexibility and decoupling.

<a name="the-exceptions-directory"></a>
### The Exceptions Directory

The `Exceptions` directory contains all of the custom exceptions for your application. These exceptions may be generated using the `make:exception` command.

<a name="the-http-directory"></a>
### The Http Directory

The `Http` directory contains your controllers, middleware, and form requests. Almost all of the logic to handle requests entering your application will be placed in this directory.

<div style="page-break-after: always"></div>

<a name="the-jobs-directory"></a>
### The Jobs Directory

This directory does not exist by default, but will be created for you if you execute the `make:job` Artisan command. The `Jobs` directory houses the [queueable jobs](/docs/{{version}}/queues) for your application. Jobs may be queued by your application or run synchronously within the current request lifecycle. Jobs that run synchronously during the current request are sometimes referred to as "commands" since they are an implementation of the [command pattern](https://en.wikipedia.org/wiki/Command_pattern).

<a name="the-listeners-directory"></a>
### The Listeners Directory

This directory does not exist by default, but will be created for you if you execute the `event:generate` or `make:listener` Artisan commands. The `Listeners` directory contains the classes that handle your [events](/docs/{{version}}/events). Event listeners receive an event instance and perform logic in response to the event being fired. For example, a `UserRegistered` event might be handled by a `SendWelcomeEmail` listener.

<a name="the-mail-directory"></a>
### The Mail Directory

This directory does not exist by default, but will be created for you if you execute the `make:mail` Artisan command. The `Mail` directory contains all of your [classes that represent emails](/docs/{{version}}/mail) sent by your application. Mail objects allow you to encapsulate all of the logic of building an email in a single, simple class that may be sent using the `Mail::send` method.

<a name="the-models-directory"></a>
### The Models Directory

The `Models` directory contains all of your [Eloquent model classes](/docs/{{version}}/eloquent). The Eloquent ORM included with Laravel provides a beautiful, simple ActiveRecord implementation for working with your database. Each database table has a corresponding "Model" which is used to interact with that table. Models allow you to query for data in your tables, as well as insert new records into the table.

<a name="the-notifications-directory"></a>
### The Notifications Directory

This directory does not exist by default, but will be created for you if you execute the `make:notification` Artisan command. The `Notifications` directory contains all of the "transactional" [notifications](/docs/{{version}}/notifications) that are sent by your application, such as simple notifications about events that happen within your application. Laravel's notification feature abstracts sending notifications over a variety of drivers such as email, Slack, SMS, or stored in a database.

<a name="the-policies-directory"></a>
### The Policies Directory

This directory does not exist by default, but will be created for you if you execute the `make:policy` Artisan command. The `Policies` directory contains the [authorization policy classes](/docs/{{version}}/authorization) for your application. Policies are used to determine if a user can perform a given action against a resource.

<div style="page-break-after: always"></div>

<a name="the-providers-directory"></a>
### The Providers Directory

The `Providers` directory contains all of the [service providers](/docs/{{version}}/providers) for your application. Service providers bootstrap your application by binding services in the service container, registering events, or performing any other tasks to prepare your application for incoming requests.

In a fresh Laravel application, this directory will already contain the `AppServiceProvider`. You are free to add your own providers to this directory as needed.

<a name="the-rules-directory"></a>
### The Rules Directory

This directory does not exist by default, but will be created for you if you execute the `make:rule` Artisan command. The `Rules` directory contains the custom validation rule objects for your application. Rules are used to encapsulate complicated validation logic in a simple object. For more information, check out the [validation documentation](/docs/{{version}}/validation).

<div style="page-break-after: always"></div>


# Frontend

- [Introduction](#introduction)
- [Using PHP](#using-php)
    - [PHP and Blade](#php-and-blade)
    - [Livewire](#livewire)
    - [Starter Kits](#php-starter-kits)
- [Using React or Vue](#using-react-or-vue)
    - [Inertia](#inertia)
    - [Starter Kits](#inertia-starter-kits)
- [Bundling Assets](#bundling-assets)

<a name="introduction"></a>
## Introduction

Laravel is a backend framework that provides all of the features you need to build modern web applications, such as [routing](/docs/{{version}}/routing), [validation](/docs/{{version}}/validation), [caching](/docs/{{version}}/cache), [queues](/docs/{{version}}/queues), [file storage](/docs/{{version}}/filesystem), and more. However, we believe it's important to offer developers a beautiful full-stack experience, including powerful approaches for building your application's frontend.

There are two primary ways to tackle frontend development when building an application with Laravel, and which approach you choose is determined by whether you would like to build your frontend by leveraging PHP or by using JavaScript frameworks such as Vue and React. We'll discuss both of these options below so that you can make an informed decision regarding the best approach to frontend development for your application.

<div style="page-break-after: always"></div>

<a name="using-php"></a>
## Using PHP

<a name="php-and-blade"></a>
### PHP and Blade

In the past, most PHP applications rendered HTML to the browser using simple HTML templates interspersed with PHP `echo` statements which render data that was retrieved from a database during the request:

```blade
<div>
    <?php foreach ($users as $user): ?>
        Hello, <?php echo $user->name; ?> <br />
    <?php endforeach; ?>
</div>
```

In Laravel, this approach to rendering HTML can still be achieved using [views](/docs/{{version}}/views) and [Blade](/docs/{{version}}/blade). Blade is an extremely light-weight templating language that provides convenient, short syntax for displaying data, iterating over data, and more:

```blade
<div>
    @foreach ($users as $user)
        Hello, {{ $user->name }} <br />
    @endforeach
</div>
```

When building applications in this fashion, form submissions and other page interactions typically receive an entirely new HTML document from the server and the entire page is re-rendered by the browser. Even today, many applications may be perfectly suited to having their frontends constructed in this way using simple Blade templates.

<a name="growing-expectations"></a>
#### Growing Expectations

However, as user expectations regarding web applications have matured, many developers have found the need to build more dynamic frontends with interactions that feel more polished. In light of this, some developers choose to begin building their application's frontend using JavaScript frameworks such as Vue and React.

Others, preferring to stick with the backend language they are comfortable with, have developed solutions that allow the construction of modern web application UIs while still primarily utilizing their backend language of choice. For example, in the [Rails](https://rubyonrails.org/) ecosystem, this has spurred the creation of libraries such as [Turbo](https://turbo.hotwired.dev/) [Hotwire](https://hotwired.dev/), and [Stimulus](https://stimulus.hotwired.dev/).

Within the Laravel ecosystem, the need to create modern, dynamic frontends by primarily using PHP has led to the creation of [Laravel Livewire](https://livewire.laravel.com) and [Alpine.js](https://alpinejs.dev/).

<div style="page-break-after: always"></div>

<a name="livewire"></a>
### Livewire

[Laravel Livewire](https://livewire.laravel.com) is a framework for building Laravel powered frontends that feel dynamic, modern, and alive just like frontends built with modern JavaScript frameworks like Vue and React.

When using Livewire, you will create Livewire "components" that render a discrete portion of your UI and expose methods and data that can be invoked and interacted with from your application's frontend. For example, a simple "Counter" component might look like the following:

```php
namespace App\Http\Livewire;

use Livewire\Component;

class Counter extends Component
{
    public $count = 0;

    public function increment()
    {
        $this->count++;
    }

    public function render()
    {
        return view('livewire.counter');
    }
}
```

And, the corresponding template for the counter would be written like so:

```blade
<div>
    <button wire:click="increment">+</button>
    <h1>{{ $count }}</h1>
</div>
```

As you can see, Livewire enables you to write new HTML attributes such as `wire:click` that connect your Laravel application's frontend and backend. In addition, you can render your component's current state using simple Blade expressions.

For many, Livewire has revolutionized frontend development with Laravel, allowing them to stay within the comfort of Laravel while constructing modern, dynamic web applications. Typically, developers using Livewire will also utilize [Alpine.js](https://alpinejs.dev/) to "sprinkle" JavaScript onto their frontend only where it is needed, such as in order to render a dialog window.

If you're new to Laravel, we recommend getting familiar with the basic usage of [views](/docs/{{version}}/views) and [Blade](/docs/{{version}}/blade). Then, consult the official [Laravel Livewire documentation](https://livewire.laravel.com/docs) to learn how to take your application to the next level with interactive Livewire components.

<div style="page-break-after: always"></div>

<a name="php-starter-kits"></a>
### Starter Kits

If you would like to build your frontend using PHP and Livewire, you can leverage our [Livewire starter kit](/docs/{{version}}/starter-kits) to jump-start your application's development.

<a name="using-react-or-vue"></a>
## Using React or Vue

Although it's possible to build modern frontends using Laravel and Livewire, many developers still prefer to leverage the power of a JavaScript framework like React or Vue. This allows developers to take advantage of the rich ecosystem of JavaScript packages and tools available via NPM.

However, without additional tooling, pairing Laravel with React or Vue would leave us needing to solve a variety of complicated problems such as client-side routing, data hydration, and authentication. Client-side routing is often simplified by using opinionated React / Vue frameworks such as [Next](https://nextjs.org/) and [Nuxt](https://nuxt.com/); however, data hydration and authentication remain complicated and cumbersome problems to solve when pairing a backend framework like Laravel with these frontend frameworks.

In addition, developers are left maintaining two separate code repositories, often needing to coordinate maintenance, releases, and deployments across both repositories. While these problems are not insurmountable, we don't believe it's a productive or enjoyable way to develop applications.

<a name="inertia"></a>
### Inertia

Thankfully, Laravel offers the best of both worlds. [Inertia](https://inertiajs.com) bridges the gap between your Laravel application and your modern React or Vue frontend, allowing you to build full-fledged, modern frontends using React or Vue while leveraging Laravel routes and controllers for routing, data hydration, and authentication — all within a single code repository. With this approach, you can enjoy the full power of both Laravel and React / Vue without crippling the capabilities of either tool.

After installing Inertia into your Laravel application, you will write routes and controllers like normal. However, instead of returning a Blade template from your controller, you will return an Inertia page:

<div style="page-break-after: always"></div>

```php
<?php

namespace App\Http\Controllers;

use App\Models\User;
use Inertia\Inertia;
use Inertia\Response;

class UserController extends Controller
{
    /**
     * Show the profile for a given user.
     */
    public function show(string $id): Response
    {
        return Inertia::render('users/show', [
            'user' => User::findOrFail($id)
        ]);
    }
}
```

An Inertia page corresponds to a React or Vue component, typically stored within the `resources/js/pages` directory of your application. The data given to the page via the `Inertia::render` method will be used to hydrate the "props" of the page component:

```jsx
import Layout from '@/layouts/authenticated';
import { Head } from '@inertiajs/react';

export default function Show({ user }) {
    return (
        <Layout>
            <Head title="Welcome" />
            <h1>Welcome</h1>
            <p>Hello {user.name}, welcome to Inertia.</p>
        </Layout>
    )
}
```

As you can see, Inertia allows you to leverage the full power of React or Vue when building your frontend, while providing a light-weight bridge between your Laravel powered backend and your JavaScript powered frontend.

<div style="page-break-after: always"></div>

#### Server-Side Rendering

If you're concerned about diving into Inertia because your application requires server-side rendering, don't worry. Inertia offers [server-side rendering support](https://inertiajs.com/server-side-rendering). And, when deploying your application via [Laravel Cloud](https://cloud.laravel.com) or [Laravel Forge](https://forge.laravel.com), it's a breeze to ensure that Inertia's server-side rendering process is always running.

<a name="inertia-starter-kits"></a>
### Starter Kits

If you would like to build your frontend using Inertia and Vue / React, you can leverage our [React or Vue application starter kits](/docs/{{version}}/starter-kits) to jump-start your application's development. Both of these starter kits scaffold your application's backend and frontend authentication flow using Inertia, Vue / React, [Tailwind](https://tailwindcss.com), and [Vite](https://vitejs.dev) so that you can start building your next big idea.

<a name="bundling-assets"></a>
## Bundling Assets

Regardless of whether you choose to develop your frontend using Blade and Livewire or Vue / React and Inertia, you will likely need to bundle your application's CSS into production ready assets. Of course, if you choose to build your application's frontend with Vue or React, you will also need to bundle your components into browser ready JavaScript assets.

By default, Laravel utilizes [Vite](https://vitejs.dev) to bundle your assets. Vite provides lightning-fast build times and near instantaneous Hot Module Replacement (HMR) during local development. In all new Laravel applications, including those using our [starter kits](/docs/{{version}}/starter-kits), you will find a `vite.config.js` file that loads our light-weight Laravel Vite plugin that makes Vite a joy to use with Laravel applications.

The fastest way to get started with Laravel and Vite is by beginning your application's development using [our application starter kits](/docs/{{version}}/starter-kits), which jump-starts your application by providing frontend and backend authentication scaffolding.

> [!NOTE]
> For more detailed documentation on utilizing Vite with Laravel, please see our [dedicated documentation on bundling and compiling your assets](/docs/{{version}}/vite).

<div style="page-break-after: always"></div>


# Starter Kits

- [Introduction](#introduction)
- [Creating an Application Using a Starter Kit](#creating-an-application)
- [Available Starter Kits](#available-starter-kits)
    - [React](#react)
    - [Vue](#vue)
    - [Livewire](#livewire)
- [Starter Kit Customization](#starter-kit-customization)
    - [React](#react-customization)
    - [Vue](#vue-customization)
    - [Livewire](#livewire-customization)
- [WorkOS AuthKit Authentication](#workos)
- [Inertia SSR](#inertia-ssr)
- [Community Maintained Starter Kits](#community-maintained-starter-kits)
- [Frequently Asked Questions](#faqs)

<a name="introduction"></a>
## Introduction

To give you a head start building your new Laravel application, we are happy to offer [application starter kits](https://laravel.com/starter-kits). These starter kits give you a head start on building your next Laravel application, and include the routes, controllers, and views you need to register and authenticate your application's users.

While you are welcome to use these starter kits, they are not required. You are free to build your own application from the ground up by simply installing a fresh copy of Laravel. Either way, we know you will build something great!

<a name="creating-an-application"></a>
## Creating an Application Using a Starter Kit

To create a new Laravel application using one of our starter kits, you should first [install PHP and the Laravel CLI tool](/docs/{{version}}/installation#installing-php). If you already have PHP and Composer installed, you may install the Laravel installer CLI tool via Composer:

```shell
composer global require laravel/installer
```

Then, create a new Laravel application using the Laravel installer CLI. The Laravel installer will prompt you to select your preferred starter kit:

```shell
laravel new my-app
```
<div style="page-break-after: always"></div>

After creating your Laravel application, you only need to install its frontend dependencies via NPM and start the Laravel development server:

```shell
cd my-app
npm install && npm run build
composer run dev
```

Once you have started the Laravel development server, your application will be accessible in your web browser at [http://localhost:8000](http://localhost:8000).

<a name="available-starter-kits"></a>
## Available Starter Kits

<a name="react"></a>
### React

Our React starter kit provides a robust, modern starting point for building Laravel applications with a React frontend using [Inertia](https://inertiajs.com).

Inertia allows you to build modern, single-page React applications using classic server-side routing and controllers. This lets you enjoy the frontend power of React combined with the incredible backend productivity of Laravel and lightning-fast Vite compilation.

The React starter kit utilizes React 19, TypeScript, Tailwind, and the [shadcn/ui](https://ui.shadcn.com) component library.

<a name="vue"></a>
### Vue

Our Vue starter kit provides a great starting point for building Laravel applications with a Vue frontend using [Inertia](https://inertiajs.com).

Inertia allows you to build modern, single-page Vue applications using classic server-side routing and controllers. This lets you enjoy the frontend power of Vue combined with the incredible backend productivity of Laravel and lightning-fast Vite compilation.

The Vue starter kit utilizes the Vue Composition API, TypeScript, Tailwind, and the [shadcn-vue](https://www.shadcn-vue.com/) component library.

<a name="livewire"></a>
### Livewire

Our Livewire starter kit provides the perfect starting point for building Laravel applications with a [Laravel Livewire](https://livewire.laravel.com) frontend.

Livewire is a powerful way of building dynamic, reactive, frontend UIs using just PHP. It's a great fit for teams that primarily use Blade templates and are looking for a simpler alternative to JavaScript-driven SPA frameworks like React and Vue.

The Livewire starter kit utilizes Livewire, Tailwind, and the [Flux UI](https://fluxui.dev) component library.

<div style="page-break-after: always"></div>

<a name="starter-kit-customization"></a>
## Starter Kit Customization

<a name="react-customization"></a>
### React

Our React starter kit is built with Inertia 2, React 19, Tailwind 4, and [shadcn/ui](https://ui.shadcn.com). As with all of our starter kits, all of the backend and frontend code exists within your application to allow for full customization.

The majority of the frontend code is located in the `resources/js` directory. You are free to modify any of the code to customize the appearance and behavior of your application:

```text
resources/js/
├── components/    # Reusable React components
├── hooks/         # React hooks
├── layouts/       # Application layouts
├── lib/           # Utility functions and configuration
├── pages/         # Page components
└── types/         # TypeScript definitions
```

To publish additional shadcn components, first [find the component you want to publish](https://ui.shadcn.com). Then, publish the component using `npx`:

```shell
npx shadcn@latest add switch
```

In this example, the command will publish the Switch component to `resources/js/components/ui/switch.tsx`. Once the component has been published, you can use it in any of your pages:

```jsx
import { Switch } from "@/components/ui/switch"

const MyPage = () => {
  return (
    <div>
      <Switch />
    </div>
  );
};

export default MyPage;
```

<div style="page-break-after: always"></div>

<a name="react-available-layouts"></a>
#### Available Layouts

The React starter kit includes two different primary layouts for you to choose from: a "sidebar" layout and a "header" layout. The sidebar layout is the default, but you can switch to the header layout by modifying the layout that is imported at the top of your application's `resources/js/layouts/app-layout.tsx` file:

```js
import AppLayoutTemplate from '@/layouts/app/app-sidebar-layout'; // [tl! remove]
import AppLayoutTemplate from '@/layouts/app/app-header-layout'; // [tl! add]
```

<a name="react-sidebar-variants"></a>
#### Sidebar Variants

The sidebar layout includes three different variants: the default sidebar variant, the "inset" variant, and the "floating" variant. You may choose the variant you like best by modifying the `resources/js/components/app-sidebar.tsx` component:

```text
<Sidebar collapsible="icon" variant="sidebar"> [tl! remove]
<Sidebar collapsible="icon" variant="inset"> [tl! add]
```

<a name="react-authentication-page-layout-variants"></a>
#### Authentication Page Layout Variants

The authentication pages included with the React starter kit, such as the login page and registration page, also offer three different layout variants: "simple", "card", and "split".

To change your authentication layout, modify the layout that is imported at the top of your application's `resources/js/layouts/auth-layout.tsx` file:

```js
import AuthLayoutTemplate from '@/layouts/auth/auth-simple-layout'; // [tl! remove]
import AuthLayoutTemplate from '@/layouts/auth/auth-split-layout'; // [tl! add]
```

<div style="page-break-after: always"></div>

<a name="vue-customization"></a>
### Vue

Our Vue starter kit is built with Inertia 2, Vue 3 Composition API, Tailwind, and [shadcn-vue](https://www.shadcn-vue.com/). As with all of our starter kits, all of the backend and frontend code exists within your application to allow for full customization.

The majority of the frontend code is located in the `resources/js` directory. You are free to modify any of the code to customize the appearance and behavior of your application:

```text
resources/js/
├── components/    # Reusable Vue components
├── composables/   # Vue composables / hooks
├── layouts/       # Application layouts
├── lib/           # Utility functions and configuration
├── pages/         # Page components
└── types/         # TypeScript definitions
```

To publish additional shadcn-vue components, first [find the component you want to publish](https://www.shadcn-vue.com). Then, publish the component using `npx`:

```shell
npx shadcn-vue@latest add switch
```

In this example, the command will publish the Switch component to `resources/js/components/ui/Switch.vue`. Once the component has been published, you can use it in any of your pages:

```vue
<script setup lang="ts">
import { Switch } from '@/Components/ui/switch'
</script>

<template>
    <div>
        <Switch />
    </div>
</template>
```

<a name="vue-available-layouts"></a>
#### Available Layouts

The Vue starter kit includes two different primary layouts for you to choose from: a "sidebar" layout and a "header" layout. The sidebar layout is the default, but you can switch to the header layout by modifying the layout that is imported at the top of your application's `resources/js/layouts/AppLayout.vue` file:

```js
import AppLayout from '@/layouts/app/AppSidebarLayout.vue'; // [tl! remove]
import AppLayout from '@/layouts/app/AppHeaderLayout.vue'; // [tl! add]
```

<div style="page-break-after: always"></div>

<a name="vue-sidebar-variants"></a>
#### Sidebar Variants

The sidebar layout includes three different variants: the default sidebar variant, the "inset" variant, and the "floating" variant. You may choose the variant you like best by modifying the `resources/js/components/AppSidebar.vue` component:

```text
<Sidebar collapsible="icon" variant="sidebar"> [tl! remove]
<Sidebar collapsible="icon" variant="inset"> [tl! add]
```

<a name="vue-authentication-page-layout-variants"></a>
#### Authentication Page Layout Variants

The authentication pages included with the Vue starter kit, such as the login page and registration page, also offer three different layout variants: "simple", "card", and "split".

To change your authentication layout, modify the layout that is imported at the top of your application's `resources/js/layouts/AuthLayout.vue` file:

```js
import AuthLayout from '@/layouts/auth/AuthSimpleLayout.vue'; // [tl! remove]
import AuthLayout from '@/layouts/auth/AuthSplitLayout.vue'; // [tl! add]
```


<a name="livewire-customization"></a>
### Livewire

Our Livewire starter kit is built with Livewire 3, Tailwind, and [Flux UI](https://fluxui.dev/). As with all of our starter kits, all of the backend and frontend code exists within your application to allow for full customization.

#### Livewire and Volt

The majority of the frontend code is located in the `resources/views` directory. You are free to modify any of the code to customize the appearance and behavior of your application:

```text
resources/views
├── components            # Reusable Livewire components
├── flux                  # Customized Flux components
├── livewire              # Livewire pages
├── partials              # Reusable Blade partials
├── dashboard.blade.php   # Authenticated user dashboard
├── welcome.blade.php     # Guest user welcome page
```

#### Traditional Livewire Components

The frontend code is located in the `resouces/views` directory, while the `app/Livewire` directory contains the corresponding backend logic for the Livewire components.

<div style="page-break-after: always"></div>

<a name="livewire-available-layouts"></a>
#### Available Layouts

The Livewire starter kit includes two different primary layouts for you to choose from: a "sidebar" layout and a "header" layout. The sidebar layout is the default, but you can switch to the header layout by modifying the layout that is used by your application's `resources/views/components/layouts/app.blade.php` file. In addition, you should add the `container` attribute to the main Flux component:

```blade
<x-layouts.app.header>
    <flux:main container>
        {{ $slot }}
    </flux:main>
</x-layouts.app.header>
```

<a name="livewire-authentication-page-layout-variants"></a>
#### Authentication Page Layout Variants

The authentication pages included with the Livewire starter kit, such as the login page and registration page, also offer three different layout variants: "simple", "card", and "split".

To change your authentication layout, modify the layout that is used by your application's `resources/views/components/layouts/auth.blade.php` file:

```blade
<x-layouts.auth.split>
    {{ $slot }}
</x-layouts.auth.split>
```
<div style="page-break-after: always"></div>

<a name="workos"></a>
## WorkOS AuthKit Authentication

By default, the React, Vue, and Livewire starter kits all utilize Laravel's built-in authentication system to offer login, registration, password reset, email verification, and more. In addition, we also offer a [WorkOS AuthKit](https://authkit.com) powered variant of each starter kit that offers:

<div class="content-list" markdown="1">

- Social authentication (Google, Microsoft, GitHub, and Apple)
- Passkey authentication
- Email based "Magic Auth"
- SSO

</div>

Using WorkOS as your authentication provider [requires a WorkOS account](https://workos.com). WorkOS offers free authentication for applications up to 1 million monthly active users.

To use WorkOS AuthKit as your application's authentication provider, select the WorkOS option when creating your new starter kit powered application via `laravel new`.

### Configuring Your WorkOS Starter Kit

After creating a new application using a WorkOS powered starter kit, you should set the `WORKOS_CLIENT_ID`, `WORKOS_API_KEY`, and `WORKOS_REDIRECT_URL` environment variables in your application's `.env` file. These variables should match the values provided to you in the WorkOS dashboard for your application:

```ini
WORKOS_CLIENT_ID=your-client-id
WORKOS_API_KEY=your-api-key
WORKOS_REDIRECT_URL="${APP_URL}/authenticate"
```

Additionally, you should configure the application homepage URL in your WorkOS dashboard. This URL is where users will be redirected after they log out of your application.

<a name="configuring-authkit-authentication-methods"></a>
#### Configuring AuthKit Authentication Methods

When using a WorkOS powered starter kit, we recommend that you disable "Email + Password" authentication within your application's WorkOS AuthKit configuration settings, allowing users to only authenticate via social authentication providers, passkeys, "Magic Auth", and SSO. This allows your application to totally avoid handling user passwords.

<a name="configuring-authkit-session-timeouts"></a>
#### Configuring AuthKit Session Timeouts

In addition, we recommend that you configure your WorkOS AuthKit session inactivity timeout to match your Laravel application's configured session timeout threshold, which is typically two hours.

<div style="page-break-after: always"></div>

<a name="inertia-ssr"></a>
### Inertia SSR

The React and Vue starter kits are compatible with Inertia's [server-side rendering](https://inertiajs.com/server-side-rendering) capabilities. To build an Inertia SSR compatible bundle for your application, run the `build:ssr` command:

```shell
npm run build:ssr
```

For convenience, a `composer dev:ssr` command is also available. This command will start the Laravel development server and Inertia SSR server after building an SSR compatible bundle for your application, allowing you to test your application locally using Inertia's server-side rendering engine:

```shell
composer dev:ssr
```

<a name="community-maintained-starter-kits"></a>
### Community Maintained Starter Kits

When creating a new Laravel application using the Laravel installer, you may provide any community maintained starter kit available on Packagist to the `--using` flag:

```shell
laravel new my-app --using=example/starter-kit
```

<a name="creating-starter-kits"></a>
#### Creating Starter Kits

To ensure your starter kit is available to others, you will need to publish it to [Packagist](https://packagist.org). Your starter kit should define its required environment variables in its `.env.example` file, and any necessary post-installation commands should be listed in the `post-create-project-cmd` array of the starter kit's `composer.json` file.

<div style="page-break-after: always"></div>

<a name="faqs"></a>
### Frequently Asked Questions

<a name="faq-upgrade"></a>
#### How do I upgrade?

Every starter kit gives you a solid starting point for your next application. With full ownership of the code, you can tweak, customize, and build your application exactly as you envision. However, there is no need to update the starter kit itself.

<a name="faq-enable-email-verification"></a>
#### How do I enable email verification?

Email verification can be added by uncommenting the `MustVerifyEmail` import in your `App/Models/User.php` model and ensuring the model implements the `MustVerifyEmail` interface:

```php
namespace App\Models;

use Illuminate\Contracts\Auth\MustVerifyEmail;
// ...

class User extends Authenticatable implements MustVerifyEmail
{
    // ...
}
```

After registration, users will receive a verification email. To restrict access to certain routes until the user's email address is verified, add the `verified` middleware to the routes:

```php
Route::middleware(['auth', 'verified'])->group(function () {
    Route::get('dashboard', function () {
        return Inertia::render('dashboard');
    })->name('dashboard');
});
```

> [!NOTE]
> Email verification is not required when using the [WorkOS](#workos) variant of the starter kits.

<a name="faq-modify-email-template"></a>
#### How do I modify the default email template?

You may want to customize the default email template to better align with your application's branding. To modify this template, you should publish the email views to your application with the following command:

```
php artisan vendor:publish --tag=laravel-mail
```

This will generate several files in `resources/views/vendor/mail`. You can modify any of these files as well as the `resources/views/vendor/mail/themes/default.css` file to change the look and appearance of the default email template.

<div style="page-break-after: always"></div>


# Deployment

- [Introduction](#introduction)
- [Server Requirements](#server-requirements)
- [Server Configuration](#server-configuration)
    - [Nginx](#nginx)
    - [FrankenPHP](#frankenphp)
    - [Directory Permissions](#directory-permissions)
- [Optimization](#optimization)
    - [Caching Configuration](#optimizing-configuration-loading)
    - [Caching Events](#caching-events)
    - [Caching Routes](#optimizing-route-loading)
    - [Caching Views](#optimizing-view-loading)
- [Debug Mode](#debug-mode)
- [The Health Route](#the-health-route)
- [Deploying With Laravel Cloud or Forge](#deploying-with-cloud-or-forge)

<a name="introduction"></a>
## Introduction

When you're ready to deploy your Laravel application to production, there are some important things you can do to make sure your application is running as efficiently as possible. In this document, we'll cover some great starting points for making sure your Laravel application is deployed properly.

<a name="server-requirements"></a>
## Server Requirements

The Laravel framework has a few system requirements. You should ensure that your web server has the following minimum PHP version and extensions:

<div class="content-list" markdown="1">

- PHP >= 8.2
- Ctype PHP Extension
- cURL PHP Extension
- DOM PHP Extension
- Fileinfo PHP Extension
- Filter PHP Extension
- Hash PHP Extension
- Mbstring PHP Extension
- OpenSSL PHP Extension
- PCRE PHP Extension
- PDO PHP Extension
- Session PHP Extension
- Tokenizer PHP Extension
- XML PHP Extension

</div>

<div style="page-break-after: always"></div>

<a name="server-configuration"></a>
## Server Configuration

<a name="nginx"></a>
### Nginx

If you are deploying your application to a server that is running Nginx, you may use the following configuration file as a starting point for configuring your web server. Most likely, this file will need to be customized depending on your server's configuration. **If you would like assistance in managing your server, consider using a fully-managed Laravel platform like [Laravel Cloud](https://cloud.laravel.com).**

Please ensure, like the configuration below, your web server directs all requests to your application's `public/index.php` file. You should never attempt to move the `index.php` file to your project's root, as serving the application from the project root will expose many sensitive configuration files to the public Internet:

```nginx
server {
    listen 80;
    listen [::]:80;
    server_name example.com;
    root /srv/example.com/public;

    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-Content-Type-Options "nosniff";

    index index.php;

    charset utf-8;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location = /favicon.ico { access_log off; log_not_found off; }
    location = /robots.txt  { access_log off; log_not_found off; }

    error_page 404 /index.php;

    location ~ ^/index\.php(/|$) {
        fastcgi_pass unix:/var/run/php/php8.2-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
        fastcgi_hide_header X-Powered-By;
    }

    location ~ /\.(?!well-known).* {
        deny all;
    }
}
```

<div style="page-break-after: always"></div>

<a name="frankenphp"></a>
### FrankenPHP

[FrankenPHP](https://frankenphp.dev/) may also be used to serve your Laravel applications. FrankenPHP is a modern PHP application server written in Go. To serve a Laravel PHP application using FrankenPHP, you may simply invoke its `php-server` command:

```shell
frankenphp php-server -r public/
```

To take advantage of more powerful features supported by FrankenPHP, such as its [Laravel Octane](/docs/{{version}}/octane) integration, HTTP/3, modern compression, or the ability to package Laravel applications as standalone binaries, please consult FrankenPHP's [Laravel documentation](https://frankenphp.dev/docs/laravel/).

<a name="directory-permissions"></a>
### Directory Permissions

Laravel will need to write to the `bootstrap/cache` and `storage` directories, so you should ensure the web server process owner has permission to write to these directories.

<a name="optimization"></a>
## Optimization

When deploying your application to production, there are a variety of files that should be cached, including your configuration, events, routes, and views. Laravel provides a single, convenient `optimize` Artisan command that will cache all of these files. This command should typically be invoked as part of your application's deployment process:

```shell
php artisan optimize
```

The `optimize:clear` method may be used to remove all of the cache files generated by the `optimize` command as well as all keys in the default cache driver:

```shell
php artisan optimize:clear
```

In the following documentation, we will discuss each of the granular optimization commands that are executed by the `optimize` command.

<div style="page-break-after: always"></div>

<a name="optimizing-configuration-loading"></a>
### Caching Configuration

When deploying your application to production, you should make sure that you run the `config:cache` Artisan command during your deployment process:

```shell
php artisan config:cache
```

This command will combine all of Laravel's configuration files into a single, cached file, which greatly reduces the number of trips the framework must make to the filesystem when loading your configuration values.

> [!WARNING]
> If you execute the `config:cache` command during your deployment process, you should be sure that you are only calling the `env` function from within your configuration files. Once the configuration has been cached, the `.env` file will not be loaded and all calls to the `env` function for `.env` variables will return `null`.

<a name="caching-events"></a>
### Caching Events

You should cache your application's auto-discovered event to listener mappings during your deployment process. This can be accomplished by invoking the `event:cache` Artisan command during deployment:

```shell
php artisan event:cache
```

<a name="optimizing-route-loading"></a>
### Caching Routes

If you are building a large application with many routes, you should make sure that you are running the `route:cache` Artisan command during your deployment process:

```shell
php artisan route:cache
```

This command reduces all of your route registrations into a single method call within a cached file, improving the performance of route registration when registering hundreds of routes.

<a name="optimizing-view-loading"></a>
### Caching Views

When deploying your application to production, you should make sure that you run the `view:cache` Artisan command during your deployment process:

```shell
php artisan view:cache
```

This command precompiles all your Blade views so they are not compiled on demand, improving the performance of each request that returns a view.

<div style="page-break-after: always"></div>

<a name="debug-mode"></a>
## Debug Mode

The debug option in your `config/app.php` configuration file determines how much information about an error is actually displayed to the user. By default, this option is set to respect the value of the `APP_DEBUG` environment variable, which is stored in your application's `.env` file.

> [!WARNING]
> **In your production environment, this value should always be `false`. If the `APP_DEBUG` variable is set to `true` in production, you risk exposing sensitive configuration values to your application's end users.**

<a name="the-health-route"></a>
## The Health Route

Laravel includes a built-in health check route that can be used to monitor the status of your application. In production, this route may be used to report the status of your application to an uptime monitor, load balancer, or orchestration system such as Kubernetes.

By default, the health check route is served at `/up` and will return a 200 HTTP response if the application has booted without exceptions. Otherwise, a 500 HTTP response will be returned. You may configure the URI for this route in your application's `bootstrap/app` file:

```php
->withRouting(
    web: __DIR__.'/../routes/web.php',
    commands: __DIR__.'/../routes/console.php',
    health: '/up', // [tl! remove]
    health: '/status', // [tl! add]
)
```

When HTTP requests are made to this route, Laravel will also dispatch a `Illuminate\Foundation\Events\DiagnosingHealth` event, allowing you to perform additional health checks relevant to your application. Within a [listener](/docs/{{version}}/events) for this event, you may check your application's database or cache status. If you detect a problem with your application, you may simply throw an exception from the listener.

<div style="page-break-after: always"></div>

<a name="deploying-with-cloud-or-forge"></a>
## Deploying With Laravel Cloud or Forge

<a name="laravel-cloud"></a>
#### Laravel Cloud

If you would like a fully-managed, auto-scaling deployment platform tuned for Laravel, check out [Laravel Cloud](https://cloud.laravel.com). Laravel Cloud is a robust deployment platform for Laravel, offering managed compute, databases, caches, and object storage.

Launch your Laravel application on Cloud and fall in love with the scalable simplicity. Laravel Cloud is fine-tuned by Laravel's creators to work seamlessly with the framework so you can keep writing your Laravel applications exactly like you're used to.

<a name="laravel-forge"></a>
#### Laravel Forge

If you prefer to manage your own servers but aren't comfortable configuring all of the various services needed to run a robust Laravel application, [Laravel Forge](https://forge.laravel.com) is a VPS server management platform for Laravel applications.

Laravel Forge can create servers on various infrastructure providers such as DigitalOcean, Linode, AWS, and more. In addition, Forge installs and manages all of the tools needed to build robust Laravel applications, such as Nginx, MySQL, Redis, Memcached, Beanstalk, and more.

<div style="page-break-after: always"></div>
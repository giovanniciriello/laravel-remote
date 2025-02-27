# Execute Artisan commands on remote servers
# Fork for php version below 8.0

[![Latest Version on Packagist](https://img.shields.io/packagist/v/spatie/laravel-remote.svg?style=flat-square)](https://packagist.org/packages/spatie/laravel-remote)
[![GitHub Tests Action Status](https://img.shields.io/github/workflow/status/spatie/laravel-remote/run-tests?label=tests)](https://github.com/spatie/laravel-remote/actions?query=workflow%3ATests+branch%3Amaster)
[![GitHub Code Style Action Status](https://img.shields.io/github/workflow/status/spatie/laravel-remote/Check%20&%20fix%20styling?label=code%20style)](https://github.com/spatie/laravel-remote/actions?query=workflow%3A"Check+%26+fix+styling"+branch%3Amaster)
[![Total Downloads](https://img.shields.io/packagist/dt/spatie/laravel-remote.svg?style=flat-square)](https://packagist.org/packages/spatie/laravel-remote)

This package provides a command to execute Artisan command on a remote server.

Here's an example that will clear the cache on the remote server.

```bash
php artisan remote cache:clear
```

## Installation

You can install the package via composer:

```bash
composer require giovanniciriello/laravel-remote --ignore-platform-reqs
```

You can publish the config file with:

```bash
php artisan vendor:publish --provider="Spatie\Remote\RemoteServiceProvider" --tag="remote-config"
```

This is the contents of the published config file:

```php
return [
    /*
     * This host will be used if none is specified
     * when executing the `remote` command.
     */
    'default_host' => 'default',

    /*
     * Here you can define the hosts where the commands should be executed.
     */
    'hosts' => [
        'default' => [
            'host' => env('REMOTE_HOST'),

            'port' => env('REMOTE_PORT', 22),

            'user' => env('REMOTE_USER'),

            /*
             * The package will cd to the given path before executing the given command.
             */
            'path' => env('REMOTE_PATH'),
        ]
    ],
];
```

## Usage

To execute a command on the remote server use the `remote` Artisan command. You can pass any artisan command that you would like to execute on the server.

Here's an example where we clear the cache.

```bash
php artisan remote cache:clear
```

### Executing raw commands

If you want to execute a bash command, use the `--raw` option.

Here we will get a list of files on the server.

```bash
php artisan remote ls --raw
```

### Using another host

You can define hosts in the config file. By default, the `default` host is used. To execute a command on another host use the `--host` option.

```bash
php artisan remote cache:clear --host=my-other-host
```

### Using options in remote commands

If you need to use flags or options in the command you're trying to execue, you can wrap the entire command in quotes:

```bash
php artisan remote --raw "ls -a"
```

## Testing

```bash
composer test
```

## Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information on what has changed recently.

## Contributing

Please see [CONTRIBUTING](.github/CONTRIBUTING.md) for details.

## Security Vulnerabilities

Please review [our security policy](../../security/policy) on how to report security vulnerabilities.

## Credits

- [Freek Van der Herten](https://github.com/freekmurze)
- [All Contributors](../../contributors)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.

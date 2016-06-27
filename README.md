# Laravel Improved Config

[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](LICENSE.md)
[![Laravel Version](https://img.shields.io/badge/laravel-5-orange.svg?style=flat-square)](http://laravel.com)

![Laravel Conf](conf.png)

Custom editable configs for Laravel 5.

This package helps you to store your additional configuration from your code in custom storage.

By default it uses JSON-file.

This is helpful when you need to edit your configuration by user from GUI. i.e. Website settings.

## Caution!

Be careful! This is version 2 of the package and fallback configuration was removed.

If you still need to use it, please install [version 1.*](https://github.com/gaaarfild/laravel-conf/tree/v1.2.2)

## Install

Add

``` JSON
"gaaarfild/laravel-conf": "2.*"
```

to your `composer.json` file into `require` section.

Then type in console

``` BASH
$ composer update
```

When update completed, add to your `config/app.conf` file to `providers` section

``` PHP
'providers' => [
    // ...
    Gaaarfild\LaravelConf\LaravelConfServiceProvider::class,
]
```

If you want to use `Conf` facade, add to same file at the `aliases` section

``` PHP
'aliases' => [
    // ...
  'Conf' => Gaaarfild\LaravelConf\ConfFacade::class,
]
```

To be able to change file location, please execute the following command in the console:

`php artisan vendor:publish --provider="Gaaarfild\LaravelConf\LaravelConfServiceProvider" --tag="config"`

Then you can edit file `config/laravel-conf.php` to set any path to file you want to.

### Publishing config file

To be able to change the path to config file and any other configurations, please execute the following command in the console:

`php artisan vendor:publish --provider="Gaaarfild\LaravelConf\LaravelConfServiceProvider" --tag="config"`

Now you will be able to set configurations in `config/laravel-conf.php`.

## Usage

### Get config value

``` php
Conf::get('key.to.retrieve', 'default_value');
```

Else will return default value.

Could be used 'dot' notation

### Save config value

``` PHP
Conf::set('key', 'value_to_save');
```

Could be used 'dot' notation

Also method `put` can be used to store multiple config values as array

``` PHP
$config = [
    'key1' => 'value1',
    'key2.subkey' => `value2`,
];
Conf::put($config);
```

### Removing key from config

``` PHP
Conf::forget('key');
```

Could be used 'dot' notation

### Get entire config

``` PHP
Conf::all();
```

### Check config key existence

``` PHP
Conf::has('key.to.check');
```

Could be used 'dot' notation

### Helper

Also helper `conf()` can be used for more convenience.

Usage is similar to build in `config()` helper.

``` PHP
conf()->set('key.subkey', 'myValue');

conf('key.subkey') // will return 'myValue'

conf('non.existing.key', 'myDefaultValue') // will return 'myDefaultValue'

$config = [
    'key1' => 'value1',
    'key2.subkey' => `value2`,
];

conf($config)
```

## Contributions

Contributions are highly appreciated.

Send your pull requests to `master` branch.


## License

The MIT License (MIT). Please see [License File](https://github.com/gaaarfild/laravel-conf/blob/master/LICENSE) for more information.


# Socialite

[![Build Status](https://travis-ci.org/socialite-manager/socialite.svg?branch=master)](https://travis-ci.org/socialite-manager/socialite)
[![MIT License](http://img.shields.io/badge/license-MIT-blue.svg?style=flat)](LICENSE)

## Introduction

This is inspired by laravel/socialite, you can easily use it without Laravel.

It possible to use it with various frameworks and middleware.

It is compatible with laravel/socialite.  
You can check the [Document](https://laravel.com/docs/5.5/socialite) of laravel.

## Core Providers

* twitter
* github
* google
* facebook
* bitbucket
* linkedin

## other

* [Instagram](https://github.com/socialite-manager/Instagram-Provider)

## Requirement

```
PHP >= 7.0
```

## Installation

```
composer require socialite-manager/socialite
```

## Basic Usage

```php
$config = [
    'client_id' => 'xxx',
    'client_secret' => 'xxx',
    'redirect' => 'http://example.com/callback.php',
];
```

`oath.php`

```php
use mosaxiv\Socialite\Socialite;

Socialite::driver('twitter', $config)->redirect();
```

`callback.php`

```php
use mosaxiv\Socialite\Socialite;

$user = Socialite::driver('twitter', $config)->user();

$user->getAvatar();
$user->getEmail();
$user->getId();
$user->getNickname();
$user->getName();
```

## Advanced Usage

`Sosialite` have options for use with framework and middleware

### Set Request

Interface: `\Psr\Http\Message\ServerRequestInterface`

```php
Socialite::driver('twitter', $config)
    ->setRequest($this->request);
```

### Set Session

need one of the following `read/write` interfaces.

|write|
|----|
|`$session->put()`|
|`$session->set()`|
|`$session->write()`|

|read|
|----|
|`$session->get()`|
|`$session->read()`|

```php
Socialite::driver('twitter', $config)
    ->setSession($this->request->getSession());
```

### Redirect psr7 response

`Psr\Http\Message\ResponseInterface` will be returned

```
Socialite::driver('twitter', $config)->psr7Redirect()
```

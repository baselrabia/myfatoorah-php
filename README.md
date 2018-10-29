# PHP Library for the [MyFatoorah API](https://myfatoorah.readme.io/docs)

[![Latest Version](https://img.shields.io/github/tag/BAWES/myfatoorah-php.svg?style=flat-square&label=release)](https://github.com/BAWES/myfatoorah-php/tags)
[![Software License](https://img.shields.io/github/license/BAWES/myfatoorah-php.svg?style=flat-square)](LICENSE)
[![Total Downloads](https://img.shields.io/packagist/dt/BAWES/myfatoorah-php.svg?style=flat-square)](https://packagist.org/packages/bawes/myfatoorah-php)


## Installation

The preferred way to install this library is through [composer](http://getcomposer.org/download/).

Either run

```bash
$ composer require bawes/myfatoorah-php:dev-master
```
or add

```json
"bawes/myfatoorah-php" : "dev-master"
```

to the require section of your application's `composer.json` file.


## Usage

First we need to decide which environment we want to use

### Step 1: Initialize based on the environment

#### Test Environment
```php
<?php
use bawes/myfatoorah/MyFatoorah;

$my = MyFatoorah::test();
```

#### Live Environment
```php
<?php
use bawes/myfatoorah/MyFatoorah;

$merchantCode = "[Your merchant code here]";
$username = "[Your merchant username here]";
$password = "[Your merchant password here]";
$my = MyFatoorah::live($merchantCode, $username, $password);
```

### Step 2: Build your request as follows
```php
<?php
use bawes/myfatoorah/MyFatoorah;

$merchantCode = "[Your merchant code here]";
$username = "[Your merchant username here]";
$password = "[Your merchant password here]";
$my = MyFatoorah::live($merchantCode, $username, $password);

$my->setPaymentMode(MyFatoorah::GATEWAY_ALL)
->setReturnUrl("https://google.com")
->setErrorReturnUrl("https://google.com")
->setCustomer("Khalid", "customer@email.com", "97738271")
->setReferenceId() //Pass unique order number or leave empty to use time()
->addProduct("iPhone", 5.350, 3)
->addProduct("Samsung", 12.000, 1)
->getPaymentLinkAndReference();

$redirectLink = $my['paymentUrl'];
$myfatoorahID = $my['paymentRef'];

```

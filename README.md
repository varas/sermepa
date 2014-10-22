Sermepa Request [![Build Status](https://travis-ci.org/killgt/sermepa.svg)](https://travis-ci.org/killgt/sermepa)
===============

PHP Sermepa request payments utility

> Fork to enable php 5.3 support

## Usage

```php
use Killgt\Sermepa\Request;

$request = new Request($fuc, $key, $useProductionEnviroment, $terminal, $businessName);

$request->setAmount(45.54);
$request->setOrder('2014abcd1234');
$request->setTransactionType(0);
$request->setCallbackURL('http://example.com/callback');
$request->setSuccessURL('http://example.com/ok');
$request->setErrorURL('http://example.com/error');
$request->setPayer('Peter Bishop');
$request->setProductDescription('The machine');

echo $request->render(); //outputs the form and auto-submit
```

### Checking the callback
```php
use Killgt\Sermepa\Request;
use Killgt\Sermepa\Exceptions\CallbackErrorException;

$request = new Request();
$request->setKey($key);

try {
    $callbackOk = $request->checkCallback($_POST);
} catch(CallbackErrorException $e) {
    // do something usefull as logging  $e->getMessage();
}

if ($callbackOk) {
    // Get $_POST['Ds_Order'] and update your order
    // } else {
    //     // Something went wrong
    //     }
    // }
}
```

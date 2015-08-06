# Omnipay: BKM Express (BETA)

**BKM Express gateway for Omnipay payment processing library**

[![Latest Stable Version](https://poser.pugx.org/yasinkuyu/omnipay-bkm/v/stable)](https://packagist.org/packages/yasinkuyu/omnipay-bkm) 
[![Total Downloads](https://poser.pugx.org/yasinkuyu/omnipay-bkm/downloads)](https://packagist.org/packages/yasinkuyu/omnipay-bkm) 
[![Latest Unstable Version](https://poser.pugx.org/yasinkuyu/omnipay-bkm/v/unstable)](https://packagist.org/packages/yasinkuyu/omnipay-bkm) 
[![License](https://poser.pugx.org/yasinkuyu/omnipay-bkm/license)](https://packagist.org/packages/yasinkuyu/omnipay-bkm)

[Omnipay](https://github.com/thephpleague/omnipay) is a framework agnostic, multi-gateway payment
processing library for PHP 5.3+. This package implements BKM Express (Turkish Payment Gateways) support for Omnipay.

BKM Express sanal pos hizmeti için omnipay kütüphanesi.

## Installation

Omnipay is installed via [Composer](http://getcomposer.org/). To install, simply add it
to your `composer.json` file:

```json
{
    "require": {
        "yasinkuyu/omnipay-bkm": "~2.0"
    }
}
```

And run composer to update your dependencies:

    $ curl -s http://getcomposer.org/installer | php
    $ php composer.phar update

## Basic Usage

The following gateways are provided by this package:

* BKM Express

Gateway Methods

* purchase($options) - authorize and immediately capture an amount on the customer's card
* refund($options) - refund an already processed transaction

For general usage instructions, please see the main [Omnipay](https://github.com/thephpleague/omnipay)
repository.

## Unit Tests

PHPUnit is a programmer-oriented testing framework for PHP. It is an instance of the xUnit architecture for unit testing frameworks.

## Sample App
        <?php defined('BASEPATH') OR exit('No direct script access allowed');

        use Omnipay\Omnipay;

        class BkmTest extends CI_Controller {

            public function index() {
                $gateway = Omnipay::create('Bkm');

                $gateway->setApiId("im0569328007a12b0c09eb1413802353");
                $gateway->setSecretKey("im061148300b91d40a48681413802353");

                $gateway->setTestMode(TRUE);

                $options = [
                    'number'        => '4242424242424242',
                    'expiryMonth'   => '10',
                    'expiryYear'    => '2015',
                    'cvv'           => '000',
                    'fistname'      => 'Yasin',
                    'lastname'      => 'Kuyu'
                ];

                $response = $gateway->purchase(
                [
                    'installment'   => 2,
                    'transId'       => '2233333333333333',
                    'amount'        => 10.00,
                    'currency'      => 'TRY',
                    'card'          => $options
                ]
                )->send();


                if ($response->isSuccessful()) {
                    echo $response->getTransactionReference();
                    echo $response->getMessage();
                }else{
                    echo $response->getError();
                } 

                // Debug
                //var_dump($response);

            }

        }


## Support

If you are having general issues with Omnipay, we suggest posting on
[Stack Overflow](http://stackoverflow.com/). Be sure to add the
[omnipay tag](http://stackoverflow.com/questions/tagged/omnipay) so it can be easily found.

If you want to keep up to date with release anouncements, discuss ideas for the project, or ask more detailed questions, there is also a [mailing list](https://groups.google.com/forum/#!forum/omnipay) which
you can subscribe to.

If you believe you have found a bug, please report it using the [GitHub issue tracker](https://github.com/yasinkuyu/omnipay-bkm/issues),
or better yet, fork the library and submit a pull request.

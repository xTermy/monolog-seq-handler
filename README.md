# Monolog [Seq](https://getseq.net/) Handler

This package provides a SeqHandler for the [Monolog](https://github.com/Seldaek/monolog) library.
[Seq](https://getseq.net/) is a log server that runs on a central machine.

Prerequisites
-------------

- PHP 8.0 or above.

Installation
------------

Install the latest version with

```bash
$ composer require stormcode/monolog-seq-handler
```

##### HTTP Clients

In order to send HTTP requests, you need a HTTP adapter. This package relies on HTTPlug which is build on top of [PSR-7](https://www.php-fig.org/psr/psr-7/)
and defines how HTTP message should be sent and received. You can use any library to send HTTP messages that
implements [php-http/client-implementation](https://packagist.org/providers/php-http/client-implementation).

Here is a list of all officially supported clients and adapters by HTTPlug: http://docs.php-http.org/en/latest/clients.html

Read more about HTTPlug in [their docs](http://docs.php-http.org/en/latest/httplug/users.html).

Basic Usage
-----------

```php
<?php

use Monolog\Logger;
use Msschl\Monolog\Handler\SeqHandler;

// create a log channel
$log = new Logger('channel-name');

// push the SeqHandler to the monolog logger.
$log->pushHandler(new SeqHandler('https://seq-server/'));

// add records to the log
$log->warning('Foo');
$log->error('Bar');
```

To authenticate or tag messages from the logger, set a Api-Key:
```php
$log->pushHandler(new SeqHandler('https://seq-server/', 'API-KEY'));
```

License
-------

This project is licensed under the terms of the MIT license.
See the [LICENSE](LICENSE.md) file for license rights and limitations.

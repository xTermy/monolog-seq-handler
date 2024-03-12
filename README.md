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

To authenticate or tag messages from the logger, set an Api-Key:
```php
$log->pushHandler(new SeqHandler('https://seq-server/', 'API-KEY'));
```

Typical Laravel Usage
---------------------
To use logs with ```Log::error('Error')``` to ```config/logging.php``` add:

```php
'seq' => [
    'driver' => 'monolog',
    'handler' => StormCode\SeqMonolog\Handler\SeqHandler::class,
    'with' => [
        'serverUri' => env('SEQ_URL'),
        'apiKey' => env('SEQ_API_KEY', null),
        'level' => Monolog\Logger::DEBUG,
        'bubble' => true
    ],
    'formatter' => StormCode\SeqMonolog\Formatter\SeqCompactJsonFormatter::class,
    'formatter_with' => [
        'batchMode' => 1, //1 OR 2
    ],
],
```
Then add this to your ```.env``` file:
```.dotenv
LOG_CHANNEL=seq

SEQ_URL=http://localhost:5341/
SEQ_API_KEY=YOUR_API_KEY
```
Now you can freely use seq

License
-------

This project is licensed under the terms of the MIT license.
See the [LICENSE](LICENSE.md) file for license rights and limitations.








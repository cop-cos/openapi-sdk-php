# An implementation of PHP for COP SDK


## Install

* To install via [Composer](http://getcomposer.org/), use the command below, it will automatically detect the latest version and bind it with `^`.

```shell
	composer require cop-cos/cop-guzzle-sdk
```

* To install via composer.json.

```json
    "require": {
        "cop-cos/cop-guzzle-sdk": "^1.0.0"
    }
```
And perform installation:

```shell
	composer install
```

## Requirements

+ PHP 7.0+
+ guzzlehttp/guzzle 7.2+

## Usage


```php
<?php
use COP\Client\COPClient;
use GuzzleHttp\Exception\RequestException;
use GuzzleHttp\HandlerStack;
/****************************************************************
 * Setting up HttpClient ...
 ***************************************************************/
$stack = HandlerStack::create();

$copClient = COPClient::builder('YOUR Api Key', 'YOUR Secret Key')->build();

$copClient->register($stack);

$httpClient = new \GuzzleHttp\Client(['handler' => $stack]);
/****************************************************************/

try {
    $resp = $httpClient->request('GET', 'https://api-pp.lines.coscoshipping.com/service/info/tracking/6103622780?numberType=bl', [ // replace with actual URL
        'headers' => [
            'Accept' => 'application/json'
        ]
    ]);

    echo $resp->getStatusCode() . ' ' . $resp->getReasonPhrase() . "\n";
    echo $resp->getBody() . "\n";
} catch (RequestException $e) {
    // handle exception.
    echo $e->getMessage() . "\n";
    if ($e->hasResponse()) {
        echo $e->getResponse()->getStatusCode() . ' ' . $e->getResponse()->getReasonPhrase() . "\n";
        echo $e->getResponse()->getBody();
    }
    return;
}
```

## License

The MIT License (MIT)

Copyright (c) 2018 Cees-Jan Kiewiet

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

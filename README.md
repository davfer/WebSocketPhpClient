# Gos WebSocket Client

[![Latest Stable Version](https://poser.pugx.org/gos/websocket-client/v/stable)](https://packagist.org/packages/gos/websocket-client) [![Total Downloads](https://poser.pugx.org/gos/websocket-client/downloads)](https://packagist.org/packages/gos/websocket-client) [![License](https://poser.pugx.org/gos/websocket-client/license)](https://packagist.org/packages/gos/websocket-client)

## About

This library has been tested with Ratchet WAMP server. It can only send messages to the server, listening for replies is not implemented.
Supported functions:
 - prefix
 - call
 - publish
 - event

## Usage

```php
use Gos\Component\WebSocketClient\Wamp\Client;

$client = new Client($host, $port);
$sessionId = $client->connect();

//establish a prefix on server
$client->prefix("calc", "http://example.com/simple/calc#");

//you can send arbitrary number of arguments
$client->call('calc', 12,14,15);

$data = [0, 1, 2];

//or array
$client->call('calc', $data);

$exclude = array($sessionId); //no sense in sending the payload to ourselves
$eligible = [...] //list of other clients ids that are eligible to receive this payload

//$payload can be scalar or array
$client->publish('topic', $payload, $exclude, $eligible);

//publish an event
$client->event('topic', $payload);
$client->disconnect();
```

## License
This software is distributed under MIT License. See LICENSE for more info.

## Original Project
[https://github.com/bazo/wamp-client](https://github.com/bazo/wamp-client)

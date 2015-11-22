# Fireplay is simple, moder and lightweight PHP framework
Simple and modern php framwork based on fast routing, phpredis caching, mongodb storage and markdown layout

## How use:
```php

// Bootstrap
define('ROOT', __DIR__.'/../');
require_once ROOT . '/bootstrap/Autoloader.Class.php';
Autoloader::init();

// Init Logging
\Storage\Log::$dst = ROOT . '/logs/application.log';

// Save sessions to Redis Cache
$sessHandler = new \Storage\Sessions();
session_set_save_handler($sessHandler);
session_start();

// Routing section
Router::get('/', function () {
    \Storage\Log::info('Someone user came to root path');
    echo \Models\Pages::get('wellcome', 60*60*2);
});

Router::get('/{id}', function ($id) {
    \Storage\Log::info('Someone user came to '.$id.' path');
    echo $id;
});

Router::get('/user/{id}/medias/{type}', function ($id, $type) {
    \Storage\Log::info('Someone user came to user path with id '.$id.' and type '.$type);
    echo $id, ' ', $type;
});

// Init Router
Router::init(function () {
    // Pass broken routes to root path 
    \Storage\Log::error('Route not found');
    header('Location: /');
});

```
Example on http://router.endem.su/

## Use it for free and wellcome to Contribute
For additional information please write ur email to alex@endem.su

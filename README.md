BitDbSession
============

Zend Framework 2 module for storing sessions in database

Installation
------------

### By cloning

Clone into `./vendor/`.

### Via Composer

`"require": { "cabrilo/bit-db-session": "dev-master" }`

### Post intallation

1. Enable the module in your `application.config.php` file:

```php
<?php
return array(
	'modules' => array(
		// ...
		'BitDbSession',
	),
	// ...
);
```

2. Create session table in your database:

```SQL
CREATE TABLE `session` (
  `id` char(32) NOT NULL DEFAULT '',
  `name` char(32) NOT NULL DEFAULT '',
  `modified` int(11) DEFAULT NULL,
  `lifetime` int(11) DEFAULT NULL,
  `data` text,
  PRIMARY KEY (`id`,`name`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

Usage
-----

Simply define your session configuration in one of your configuration files, for example ```config/autoload/session.global.php```:

```php
<?php

return array(
    'session' => array(
        'table_name' => 'session',
        'config' => array(
            'class' => 'Zend\Session\Config\SessionConfig',
            'options' => array(
                'name' => 'your_session_name',
                'remember_me_seconds' => 2592000,
                'cookie_lifetime' => 2592000,
                'gc_maxlifetime' => 2592000,
                'use_cookies' => true,
            ),
        ),
        'storage' => 'Zend\Session\Storage\SessionArrayStorage',
        'validators' => array(
            array(
                'Zend\Session\Validator\RemoteAddr',
                'Zend\Session\Validator\HttpUserAgent',
            ),
        ),
    ),
);
```

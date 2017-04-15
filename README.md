# awesome-php-package

## 日志 ( Log )

### Monolog 

PHP的一个日志类库。

链接：
- https://github.com/Seldaek/monolog  
- [PHP 类库] Monolog - Logging for PHP 5.3+ - icyfire - SegmentFault
https://segmentfault.com/a/1190000002775923

相比于其他的日志类库，它有以下的特点：

- 功能强大。可以把日志发送到文件、socket、邮箱、数据库和各种web services。
- 遵循PSR3的接口规范。可以很轻易的替换成其他遵循同一规范的日志类库。
- 良好的扩展性。通过Handler、Formatter和Processor这几个接口，可以对Monolog类库进行各种扩展和自定义。

安装最新版本：
```
composer require monolog/monolog
```

要求PHP版本为5.3以上。
``` php
<?php

use Monolog\Logger;
use Monolog\Handler\StreamHandler;

// 创建日志频道
$log = new Logger('name');
$log->pushHandler(new StreamHandler('path/to/your.log', Logger::WARNING));

// 添加日志记录
$log->addWarning('Foo');
$log->addError('Bar');
```

## 请求( Request )

### Guzzle

一个完整的HTTP客户端。

链接：

- https://github.com/guzzle/guzzle
- Guzzle, PHP HTTP client — Guzzle Documentation
http://docs.guzzlephp.org/en/latest/

### Requests

一个简单的HTTP库。

链接：

- https://github.com/rmccue/Requests
- 【PHP类库】Requests - A humble HTTP request library - icyfire - SegmentFault
https://segmentfault.com/a/1190000002867007

## ORM

## 邮件( Email )

## 图像( Imagery )

## 测试( Testing )

## 身份验证( Auth )

### oauth2-server-php

一个OAuth2服务器实现。

- http://bshaffer.github.io/oauth2-server-php-docs/
- 理解OAuth 2.0 - 阮一峰的网络日志
http://www.ruanyifeng.com/blog/2014/05/oauth_2_0.html

### jwt

JSON网络令牌库。

- http://jwt.io/
- https://github.com/lcobucci/jwt

## 定时任务

### jobby

一个 PHP 的定时任务管理器。如果你的定时任务比较多，通过jobby，你只需要在crontab里写一条即可。

- https://github.com/jobbyphp/jobby

安装：
```
$ composer require hellogerard/jobby
```

编写定时任务：
jobby.php
``` php
<?php 

require_once __DIR__ . '/vendor/autoload.php';

$jobby = new Jobby\Jobby();

// Every job has a name
$jobby->add('CommandExample', [
    // Run a shell commands
    'command'  => 'ls',

    // Ordinary crontab schedule format is supported.
    // This schedule runs every hour.
    // You could also insert DateTime string in the format of Y-m-d H:i:s.
    'schedule' => '0 * * * *',

    // Stdout and stderr is sent to the specified file
    'output'   => 'logs/command.log',

    // You can turn off a job by setting 'enabled' to false
    'enabled'  => true,
]);

$jobby->add('ClosureExample', [
    // Invoke PHP closures
    'closure'  => function() {
        echo "I'm a function!\n";
        return true;
    },

    // This function will run every other hour
    'schedule' => '0 */2 * * *',

    'output'   => 'logs/closure.log',
]);

$jobby->run();
```

然后在crontab里添加一条记录：
```
* * * * * cd /path/to/project && php jobby.php 1>> /dev/null 2>&1
```


# PHP

<!-- TOC -->

- [PHP](#php)
    - [一、PHP是什么](#一php是什么)
    - [二、PHP安装](#二php安装)
        - [1、yum安装](#1yum安装)
        - [2、apt安装](#2apt安装)
        - [3、源码安装](#3源码安装)
    - [三、PHP 基础](#三php-基础)
        - [1、类型](#1类型)
            - [整形](#整形)
            - [字符串](#字符串)
            - [数组](#数组)
            - [PHP类型比较](#php类型比较)
        - [2、变量](#2变量)
        - [3、常量](#3常量)
            - [魔术常量](#魔术常量)
        - [4、表达式](#4表达式)
        - [5、运算符](#5运算符)
        - [6、流程控制](#6流程控制)
        - [7、函数](#7函数)
            - [可变参数](#可变参数)
            - [匿名函数](#匿名函数)
    - [四、PHP 进阶](#四php-进阶)
        - [1、类与对象](#1类与对象)
        - [2、命名空间](#2命名空间)
        - [3、异常处理](#3异常处理)
        - [4、生成器和引用](#4生成器和引用)
        - [5、预定义变量/接口](#5预定义变量接口)
        - [6、上下文（Context）选项和参数](#6上下文context选项和参数)
    - [五、PHP 实践](#五php-实践)
        - [1、多维数组变一维数组](#1多维数组变一维数组)
        - [2、Laravel中Model的`$visible`,`$hidden`原理](#2laravel中model的visiblehidden原理)
    - [六、PHP面试](#六php面试)
    - [七、PHP扩展](#七php扩展)
    - [八、PHP优化](#八php优化)
        - [1、composer自动加载](#1composer自动加载)
        - [2、composer原理](#2composer原理)
    - [九、参考资料](#九参考资料)

<!-- /TOC -->

## 一、PHP是什么

PHP（全称：PHP：Hypertext Preprocessor，即“PHP：超文本预处理器”）是一种开源的通用计算机脚本语言，尤其适用于网络开发并可嵌入HTML中使用。PHP的语法借鉴吸收C语言、Java和Perl等流行计算机语言的特点，易于一般程序员学习。PHP的主要目标是允许网络开发人员快速编写动态页面，但PHP也被用于其他很多领域。

## 二、PHP安装

### 1、yum安装

```bash
yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm
yum install yum-utils
subscription-manager repos --enable=rhel-7-server-optional-rpms
yum-config-manager --enable remi-php72
yum update
yum install php72 php72-php-fpm php72-php-gd php72-php-json php72-php-mbstring php72-php-mysqlnd php72-php-xml php72-php-xmlrpc php72-php-opcache
php -v
```

### 2、apt安装

```bash
apt -y install software-properties-common
add-apt-repository ppa:ondrej/php
apt -y update
apt install php7.2
apt install php-pear php7.2-fpm php7.2-curl php7.2-dev php7.2-gd php7.2-mbstring php7.2-zip php7.2-mysql php7.2-xml
php -v
```

### 3、源码安装

```bash
# 下载
wget http://hk1.php.net/get/php-7.2.10.tar.gz/from/this/mirror php-7.2.10.tar.gz
# 解压
tar -zxf php-7.2.10.tar.gz php-7.2.10
# 依赖
apt -y install \
build-essential \
gcc \
g++ \
autoconf \
libiconv-hook-dev \
libmcrypt-dev \
libxml2-dev \
libmysqlclient-dev \
libcurl4-openssl-dev \
libjpeg8-dev \
libfreetype6-dev \
libssl-dev
# 编译
./configure --prefix=/usr/local/php7.2 \
--with-config-file-path=/etc/php7.2 \
--enable-fpm \
--enable-pcntl \
--enable-mysqlnd \
--enable-opcache \
--enable-sockets \
--enable-sysvmsg \
--enable-sysvsem \
--enable-sysvshm \
--enable-shmop \
--enable-zip \
--enable-soap \
--enable-xml \
--enable-mbstring \
--disable-rpath \
--disable-debug \
--disable-fileinfo \
--with-mysqli=mysqlnd \
--with-pdo-mysql=mysqlnd \
--with-pcre-regex \
--with-iconv \
--with-zlib \
--with-gd \
--with-openssl \
--with-mhash \
--with-xmlrpc \
--with-curl \
--with-imap-ssl
# 安装
make && make install
# 输出
Build complete.
Don't forget to run 'make test'.

Installing shared extensions:     /usr/local/php7.2/lib/php/extensions/no-debug-non-zts-20170718/
Installing PHP CLI binary:        /usr/local/php7.2/bin/
Installing PHP CLI man page:      /usr/local/php7.2/php/man/man1/
Installing PHP FPM binary:        /usr/local/php7.2/sbin/
Installing PHP FPM defconfig:     /usr/local/php7.2/etc/
Installing PHP FPM man page:      /usr/local/php7.2/php/man/man8/
Installing PHP FPM status page:   /usr/local/php7.2/php/php/fpm/
Installing phpdbg binary:         /usr/local/php7.2/bin/
Installing phpdbg man page:       /usr/local/php7.2/php/man/man1/
Installing PHP CGI binary:        /usr/local/php7.2/bin/
Installing PHP CGI man page:      /usr/local/php7.2/php/man/man1/
Installing build environment:     /usr/local/php7.2/lib/php/build/
Installing header files:          /usr/local/php7.2/include/php/
Installing helper programs:       /usr/local/php7.2/bin/
  program: phpize
  program: php-config
Installing man pages:             /usr/local/php7.2/php/man/man1/
  page: phpize.1
  page: php-config.1
Installing PEAR environment:      /usr/local/php7.2/lib/php/
[PEAR] Archive_Tar    - installed: 1.4.3
[PEAR] Console_Getopt - installed: 1.4.1
[PEAR] Structures_Graph- installed: 1.1.1
[PEAR] XML_Util       - installed: 1.4.2
[PEAR] PEAR           - installed: 1.10.5
Wrote PEAR system config file at: /usr/local/php7.2/etc/pear.conf
You may want to add: /usr/local/php7.2/lib/php to your php.ini include_path
/home/vps/php-7.2.10/build/shtool install -c ext/phar/phar.phar /usr/local/php7.2/bin
ln -s -f phar.phar /usr/local/php7.2/bin/phar
Installing PDO headers:           /usr/local/php7.2/include/php/ext/pdo/
# 配置
mkdir /etc/php7.2
cp php.ini-development /etc/php7.2/php.ini
export PATH=/usr/local/php7.2/bin:$PATH
export PATH=/usr/local/php7.2/sbin:$PATH
source ~/.bashrc
# 测试
php -v
```

## 三、PHP 基础

当解析一个文件时，PHP 会寻找起始和结束标记，也就是 `<?php 和 ?>`，这告诉 PHP 开始和停止解析二者之间的代码。此种解析方式使得 PHP 可以被嵌入到各种不同的文档中去，而任何起始和结束标记之外的部分都会被 PHP 解析器忽略。

```php
# 纯php文件
<?php echo "Hello World!";

```

```php
# 嵌入html中的php文件
<p><?php echo "Hello World!"; ?></p>
```

### 1、类型

PHP 支持 9 种原始数据类型。

四种标量类型：

- boolean（布尔型）
- integer（整型）
- float（浮点型，也称作 double)
- string（字符串）

三种复合类型：

- array（数组）
- object（对象）
- callable（可调用）

最后是两种特殊类型：

- resource（资源）
- NULL（无类型）

#### 整形

注意事项：

- var_dump($0x1A) //int(26) 16进制
- var_dump($9223372036854775808) //float(9.2233720368548E+18) 整数溢出自动转换成float
- var_dump(25/7)         // float(3.5714285714286) PHP中没有整除的运算符
- var_dump((int) (25/7)) // int(3) 舍弃小数部分转换为int
- var_dump(round(25/7))  // float(4) 四舍五入

#### 字符串

Heredoc结构 和 Nowdoc结构

- Heredoc结构类似于双引号字符串，Nowdoc结构是类似于单引号字符串

```php
# Heredoc结构
<?php
$s = 'yy';
$str = <<<"EOD"
$s
EOD;
var_dump($str);

输出：string(2) "yy"
```

```php
# Nowdoc结构
<?php
$s = 'yy';
$str = <<<'EOD'
$s
EOD;
var_dump($str);

输出：string(2) "$s"
```

#### 数组

PHP中的数组实际上是一个有序映射。映射是一种把 values 关联到 keys 的类型。此类型在很多方面做了优化，因此可以把它当成真正的数组，或列表（向量），散列表（是映射的一种实现），字典，集合，栈，队列以及更多可能性。由于数组元素的值也可以是另一个数组，树形结构和多维数组也是允许的。

key 可以是 integer 或者 string。value 可以是任意类型。此外 key 会有如下的强制转换：

- 包含有合法整型值的字符串会被转换为整型。例如键名 "8" 实际会被储存为 8。但是 "08" 则不会强制转换，因为其不是一个合法的十进制数值。
- 浮点数也会被转换为整型，意味着其小数部分会被舍去。例如键名 8.7 实际会被储存为 8。
- 布尔值也会被转换成整型。即键名 true 实际会被储存为 1 而键名 false 会被储存为 0。
- Null 会被转换为空字符串，即键名 null 实际会被储存为 ""。
- 数组和对象不能被用为键名。坚持这么做会导致警告：Illegal offset type。

栗子：类型强制与覆盖

```php

<?php
$arr = [
    1    => "a",
    "1"  => "b",
    1.5  => "c",
    true => "d",
];

var_dump($arr);

输出：array(1) {
  [1]=>
  string(1) "d"
}
?>

```

栗子：将目录中的文件名填充入数组

```php
<?php
$handle = opendir('.');
while (false !== ($file = readdir($handle))) {
    $files[] = $file;
}
closedir($handle);

```

#### PHP类型比较

`empty()`更符合我们的需求

### 2、变量

```php
<?php
// 静态变量只在第一次调用函数时被初始化
function test()
{
    static $a = 0;
    echo $a;
    $a++;
}

test(); // 0
test(); // 1
test(); // 2

```

### 3、常量

`define("CONSTANT", "hello world")`

`const CONSTANT = 'Hello World'`

#### 魔术常量

- `__LINE__` 文件中的当前行号
- `__FILE__` 文件的完整路径和文件名
- `__DIR__` 文件所在的目录 `dirname(__FILE__)`
- `__FUNCTION__` 函数名称
- `__CLASS__` 类的名称
- `__TRAIT__` Trait 的名字
- `__METHOD__` 类的方法名
- `__NAMESPACE__` 当前命名空间的名称

### 4、表达式

略

### 5、运算符

```php
<?php
// $a % $b 的结果和 $a 的符号相同
echo (5 % 3)."\n";           // prints 2
echo (5 % -3)."\n";          // prints 2
echo (-5 % 3)."\n";          // prints -2
echo (-5 % -3)."\n";         // prints -2
```

### 6、流程控制

略

### 7、函数

#### 可变参数

```php
<?php
// php5.6+
function sum(...$numbers) {
    $acc = 0;
    foreach ($numbers as $n) {
        $acc += $n;
    }
    return $acc;
}

echo sum(1, 2, 3, 4); //10

// php5.5
<?php
function sum() {
    $acc = 0;
    foreach (func_get_args() as $n) {
        $acc += $n;
    }
    return $acc;
}

echo sum(1, 2, 3, 4); //10
```

#### 匿名函数

```php
<?php
$greet = function($name)
{
    printf("Hello %s\n", $name);
};

$greet('World');
$greet('PHP');
```

## 四、PHP 进阶

### 1、类与对象

类的基本概念：`class`,`new`,`extends`,`::class`

属性和方法：`public`,`protected`,`private`

类常量：`self`,`parent`,`static`

自动加载：`spl_autoload_register()`

构造函数和析构函数：`__construct()`,`__destruct()`

范围解析操作符：`::`

抽象类：`abstract`

对象接口：`interface`,`implements`

Trait：`trait`

重载：`__set()`,`__get()`,`__isset()`,`__unset()`,`__call()`,`__callStatic()`

魔术方法：`__toString()`,`__invoke()`

Final：`final`

对象复制：`clone`

后期静态调用：解决了单例继承类的应用

```php
<?php
class A {
    public static function foo() {
        static::who(); // 后期静态调用
    }

    public static function who() {
        echo __CLASS__."\n";
    }
}

class B extends A {
    public static function test() {
        A::foo(); //非转发
        parent::foo(); //转发
        self::foo(); //转发
    }

    public static function who() {
        echo __CLASS__."\n";
    }
}
class C extends B {
    public static function who() {
        echo __CLASS__."\n";
    }
}

C::test();

输出：
A
C
C
```

序列化：`serialize()`,`unserialize()`

### 2、命名空间

命名空间是一种封装事物的方法

概述：`namespace`,`use`,`as`

### 3、异常处理

```php
try {
    $a = 10;
    if ($a !== '10') {
        throw new \Exception('垃圾');
    }
} catch (\Exception $e) {
    echo $e->getMessage() . "\n";
} finally {
    echo "结束\n";
}

```

### 4、生成器和引用

`yield`

```php
// 类似range()，100w数据占用内存不到1kb，而range()在php7.2下面需要占用32mb
function xRange($start, $limit, $step = 1)
{
    if ($start < $limit) {
        if ($step <= 0) {
            throw new \LogicException('Step must be +ve');
        }

        for ($i = $start; $i <= $limit; $i += $step) {
            yield $i;
        }
    } else {
        if ($step >= 0) {
            throw new \LogicException('Step must be -ve');
        }

        for ($i = $start; $i >= $limit; $i += $step) {
            yield $i;
        }
    }
}

```

`&`

```php
// $a 和 $b 在这里是完全相同的，这并不是 $a 指向了 $b 或者相反，而是 $a 和 $b 指向了同一个地方。
<?php
$a = &$b;

```

```php
// 通过引用修改变量的值
<?php
function foo(&$var)
{
    $var++;
}

$a=5;
foo($a);
echo $a; //6
```

`$this`：在一个对象的方法中，`$this`永远是调用它的对象的引用。

`global`：`$var = &$GLOBALS["var"]` unset $var 不会 unset 全局变量。

### 5、预定义变量/接口

- $GLOBALS
- $_SERVER  http://php.net/manual/zh/reserved.variables.server.php
- $_GET
- $_POST
- $_FILES
- $_COOKIE
- $_SESSION
- $_REQUEST
- $_ENV
- $argc
- $argv

```php
// 迭代对象
Iterator extends Traversable {
    /* 方法 */
    abstract public mixed current ( void )
    abstract public scalar key ( void )
    abstract public void next ( void )
    abstract public void rewind ( void )
    abstract public bool valid ( void )
}

```

```php
// 对象能像数组一样访问
ArrayAccess {
    /* 方法 */
    abstract public boolean offsetExists ( mixed $offset )
    abstract public mixed offsetGet ( mixed $offset )
    abstract public void offsetSet ( mixed $offset , mixed $value )
    abstract public void offsetUnset ( mixed $offset )
}

```

### 6、上下文（Context）选项和参数

`stream_context_create`,`file_get_contents`,`curl`

## 五、PHP 实践

### 1、多维数组变一维数组

```php

$result = [];
//无键值对
array_walk_recursive($arr, function($value) use (&$result) {
    array_push($result, $value);
});
//有键值对
array_walk_recursive($arr, function($value) use (&$result) {
    array_push($result, array_values($value));
});

```

### 2、Laravel中Model的`$visible`,`$hidden`原理

```php
array_intersect_key():使用键名比较计算数组的交集
array_flip():交换数组中的键和值
array_diff_key():使用键名比较计算数组的差集

protected function getArrayableItems(array $values)
{
    if (count($this->getVisible()) > 0) {
        $values = array_intersect_key($values, array_flip($this->getVisible()));
    }

    if (count($this->getHidden()) > 0) {
        $values = array_diff_key($values, array_flip($this->getHidden()));
    }

    return $values;
}


```

## 六、PHP面试

[PHP面试](https://github.com/OMGZui/noteBook/blob/master/level.md)

## 七、PHP扩展

按phpinfo()上的扩展解读

|扩展库|作用|
|-|-|
|date |时间库|
|dom/xml/SimpleXML/libxml |xml操作库|
|exif |相机库|
|fileinfo |文件相关库|
|filter |参数过滤库|
|ftp |ftp库|
|gd |图像库|
|hash |hash算法库|
|iconv |字符串转换库|
|imagick| 图像库|
|json |json操作库|
|mbstring |多字节字符串操作库|
|memcached |缓存库|
|mongodb |数据库|
|mysqli |数据库|
|mysqlnd |数据库|
|openssl |加密库|
|pcre |正则库|
|PDO |数据库|
|Phar |包|
|posix |多进程库|
|readline |交互库|
|redis |缓存库|
|Reflection |反射库|
|session |会话库|
|SPL |标准库|
|swoole |异步库|
|tokenizer |标记库|
|xdebug |debug库|
|Zend OPcache |缓存库|
|zlib |压缩库|

## 八、PHP优化

### 1、composer自动加载

核心函数：`spl_autoload_register()`

1. 使用类之前无需 `include / require`
2. 使用类的时候才会 `include / require`文件，实现了 `lazy loading(延迟加载)` ，避免了 `include / require` 多余文件。
3. 无需考虑引入 类的实际磁盘地址 ，实现了逻辑和实体文件的分离。

### 2、composer原理

以Laravel框架为例

目录结构：

    vendor
    ├── autoload.php    入口文件
    vendor/composer
    ├── ClassLoader.php     composer加载类
    ├── autoload_classmap.php   自动加载的最简单形式
    ├── autoload_files.php  用于加载全局函数的文件
    ├── autoload_namespaces.php     符合PSR0标准的自动加载文件
    ├── autoload_psr4.php   符合PSR4标准的自动加载文件
    ├── autoload_real.php    composer加载类的初始化
    ├── autoload_static.php     顶级命名空间初始化类
    ├── installed.json   所有的依赖库信息

第一步：`public/index.php`入口文件直接引入

```php
require __DIR__.'/../vendor/autoload.php';
```

第二步：`vendor/autoload.php`引入

```php
require_once __DIR__ . '/composer/autoload_real.php';
return ComposerAutoloaderIniteaa4bfcc04fea23ae4b766b783b56134::getLoader();
```

第三步：`vendor/composer/autoload_real.php`

```php
    public static function getLoader()
    {
        /*********************** 单例模式 ********************/
        if (null !== self::$loader) {
            return self::$loader;
        }

        /*********************** 获得自动加载核心类对象 ********************/
        spl_autoload_register(array('ComposerAutoloaderIniteaa4bfcc04fea23ae4b766b783b56134', 'loadClassLoader'), true, true);
        self::$loader = $loader = new \Composer\Autoload\ClassLoader();
        spl_autoload_unregister(array('ComposerAutoloaderIniteaa4bfcc04fea23ae4b766b783b56134', 'loadClassLoader'));

        /*********************** 初始化自动加载核心类对象 ********************/
        $useStaticLoader = PHP_VERSION_ID >= 50600 && !defined('HHVM_VERSION') && (!function_exists('zend_loader_file_encoded') || !zend_loader_file_encoded());
        // 静态初始化
        if ($useStaticLoader) {
            require_once __DIR__ . '/autoload_static.php';

            call_user_func(\Composer\Autoload\ComposerStaticIniteaa4bfcc04fea23ae4b766b783b56134::getInitializer($loader));
        } else {
            // 调用核心类接口初始化
            // PSRO使用命名空间第一个字母作为前缀索引
            $map = require __DIR__ . '/autoload_namespaces.php';
            foreach ($map as $namespace => $path) {
                $loader->set($namespace, $path);
            }

            // PSR4标准顶级命名空间映射用了两个数组，第一个和 PSR0 一样用命名空间第一个字母作为前缀索引，然后是 顶级命名空间，
            // 但是最终并不是文件路径，而是 顶级命名空间 的长度。
            // 可以将命名空间 Symfony\\Polyfill\\Mbstring\\example 前26个字符替换成目录 __DIR__ . '/..' .
            // '/symfony/polyfill-mbstring ，我们就得到了__DIR__ . '/..' . '/symfony/polyfill-mbstring/example.php，
            // 先验证磁盘上这个文件是否存在，如果不存在接着遍历。如果遍历后没有找到，则加载失败。
            $map = require __DIR__ . '/autoload_psr4.php';
            foreach ($map as $namespace => $path) {
                $loader->setPsr4($namespace, $path);
            }

            $classMap = require __DIR__ . '/autoload_classmap.php';
            if ($classMap) {
                $loader->addClassMap($classMap);
            }
        }

        /*********************** 注册自动加载核心类对象 ********************/
        $loader->register(true);

        /*********************** 自动加载全局函数 ********************/
        if ($useStaticLoader) {
            $includeFiles = Composer\Autoload\ComposerStaticIniteaa4bfcc04fea23ae4b766b783b56134::$files;
        } else {
            $includeFiles = require __DIR__ . '/autoload_files.php';
        }
        foreach ($includeFiles as $fileIdentifier => $file) {
            composerRequireeaa4bfcc04fea23ae4b766b783b56134($fileIdentifier, $file);
        }

        // 返回自动加载核心类对象
        return $loader;
    }

    public static function getInitializer(ClassLoader $loader)
    {
        // 匿名函数绑定
        return \Closure::bind(function () use ($loader) {
            $loader->prefixLengthsPsr4 = ComposerStaticIniteaa4bfcc04fea23ae4b766b783b56134::$prefixLengthsPsr4;
            $loader->prefixDirsPsr4 = ComposerStaticIniteaa4bfcc04fea23ae4b766b783b56134::$prefixDirsPsr4;
            $loader->fallbackDirsPsr4 = ComposerStaticIniteaa4bfcc04fea23ae4b766b783b56134::$fallbackDirsPsr4;
            $loader->prefixesPsr0 = ComposerStaticIniteaa4bfcc04fea23ae4b766b783b56134::$prefixesPsr0;
            $loader->classMap = ComposerStaticIniteaa4bfcc04fea23ae4b766b783b56134::$classMap;

        }, null, ClassLoader::class);
    }

```

## 九、参考资料

[php手册](http://php.net/)

title: Composer Downloader TransportException 解决方法
date: 2016-03-22 19:39:50
categories: composer,php
tags: [composer,php]
---
## 问题
有个服务是SOAP协议，所以composer引了一个包，可是给了一个异常。
```bash
[root@localhost]# composer require "artisaninweb/laravel-soap"
[Composer\Downloader\TransportException]
Your configuration does not allow connection to http://packagist.phpcomposer.com. See https://getcomposer.org/doc/06-config.md#secure-http for details.
```
看了下phpcomposer:
````html
访问了phpcomposer看到是:

secure-http
Defaults to true. If set to true only HTTPS URLs are allowed to be downloaded via Composer. If you really absolutely need HTTP access to something then you can disable it, but using Let's Encrypt to get a free SSL certificate is generally a better alternative.
```
这是要么改secure-http要么把composer地址从http改成https的节奏。

<!--more--> 

## 解决方法
#### 1. 把默认的 secure-http 改成false
```bash
composer config -g secure-http false
```
#### ２. 修改配置文件
```bash
#修改全局文件(推荐)
composer config -g repo.packagist composer https://packagist.phpcomposer.com

#修改当前配置文件
composer config repo.packagist composer https://packagist.phpcomposer.com
```
## 修改后
composer.json 文件
```json
{
    "repositories": {
        "packagist": {
            "type": "composer",
            "url": "https://packagist.phpcomposer.com"
        }
    }
}
```



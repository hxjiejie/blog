---
title: php soap 缓存引起返回错误
category: php
tag: php
---

>转自 http://ju.outofmemory.cn/entry/196921

当你实例化一个 PHP Soap 类，需要传递一个 WSDL (Web Services Description Language) 地址：

`$client = new SoapClient(‘http://example.com/services/thescript.php?wsdl‘);`

根据你的缓存设置，PHP会决定WSDL提供的内容，以及是否存入缓存中。默认的PHP缓存是 86400秒，也就是24 小时，所以默认情况下你只能24小时读取一次WSDL，正常情况下这是没有问题的。但如果接口提供方修改了接口，你又保持在调试呢？

> 什么是 WSDL? 
W3C 是这样描述的: 
WSDL is an XML format for describing network services as a set of endpoints operating on messages containing either document-oriented or procedure-oriented information.

翻译过来就是，WSDL是为开发人员提供一个查询获取想要的服务的地图。

一个基本的功能就是能够知道你的客户端可以使用哪些接口。

当WSDL无法使用？ 
如果WSDL的提供方没有告知你他们更新了WSDL服务，你的业务就会发生奇怪的事情因为你已经将WSDL缓存了24小时（PHP的默认设置）。

关闭WSDL缓存 
PHP（Linux）缓存Soap WSDL文件在 /tmp 目录。进入 php.ini 配置文件，搜索 soap.wsdlcacheenabled 。将1 变成 0. 
搜索 soap.wsdlcachettl 这个是soap缓存的生存时间。

```
soap.wsdlcacheenabled=0;
soap.wsdlcachettl=0;
```
然后，重启　php　服务。

当然，大多数情况下，你可能根本没权限修改生产环境的PHP.ini配置。这时候你就可以按下面的方法：

`ini_set("soap.wsdl_cache_enabled", 0);`
或
`$client = new SoapClient('http://somewhere.com/?wsdl', array('cache_wsdl' => WSDL_CACHE_NONE) );`


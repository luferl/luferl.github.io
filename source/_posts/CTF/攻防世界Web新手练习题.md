---
title: 攻防世界Web新手练习题
date: 2021-08-11 00:17:19
tags: [CTF,Web]
categories: CTF
---
# view_source
## 题目
&emsp;&emsp;难度系数：1.0   
&emsp;&emsp;题目来源： Cyberpeace-n3k0  
&emsp;&emsp;题目描述：X老师让小宁同学查看一个网页的源代码，但小宁同学发现鼠标右键好像不管用了  
## 解答
&emsp;&emsp;F12得到答案：`cyberpeace{0d141ae981465634833f8446a771e484}`。
# robots
## 题目
&emsp;&emsp;难度系数： 1.0   
&emsp;&emsp;题目来源： Cyberpeace-n3k0  
&emsp;&emsp;题目描述：X老师上课讲了Robots协议，小宁同学却上课打了瞌睡，赶紧来教教小宁Robots协议是什么吧。  
## 解答
&emsp;&emsp;根据题目所说robots协议，访问场景下的`/robots.txt`文件，得到如下内容：

>User-agent: *  
Disallow:   
Disallow: f1ag_1s_h3re.php  
 
&emsp;&emsp;再访问`/f1ag_1s_h3re.php`。得到答案:`cyberpeace{b18c54f0bf9f4a64c0aecff3248d6650}`。

# backup
## 题目
&emsp;&emsp;难度系数： 1.0  
&emsp;&emsp;题目来源： Cyberpeace-n3k0  
&emsp;&emsp;题目描述：X老师忘记删除备份文件，他派小宁同学去把备份文件找出来,一起来帮小宁同学吧！
## 解答 
&emsp;&emsp;根据页面描述：`你知道index.php的备份文件名吗？`，尝试访问`index.php.bak`，下载后打开得到答案：`Cyberpeace{855A1C4B3401294CB6604CCC98BDE334}`。

# cookie
## 题目
&emsp;&emsp;难度系数： 1.0  
&emsp;&emsp;题目来源： Cyberpeace-n3k0   
&emsp;&emsp;题目描述：X老师告诉小宁他在cookie里放了些东西，小宁疑惑地想：‘这是夹心饼干的意思吗？’
## 解答
&emsp;&emsp;根据题目描述，F12查看网络请求的cookie，得到`look-here=cookie.php`。  
&emsp;&emsp;访问cookie.php，得到提示`See the http response`，根据提示查看response，在响应头中可以找到答案：`flag: cyberpeace{f9bb6af749eaf0a1877956e6c8944722}`。

# disabled_button
## 题目
&emsp;&emsp;难度系数： 1.0  
&emsp;&emsp;题目来源： Cyberpeace-n3k0  
&emsp;&emsp;题目描述：X老师今天上课讲了前端知识，然后给了大家一个不能按的按钮，小宁惊奇地发现这个按钮按不下去，到底怎么才能按下去呢？ 
## 解答
&emsp;&emsp;把button的disabled属性去掉，点击后得到答案：`cyberpeace{aa004bdc9907bdf379f228c385542b7a}`。

# weak_auth
## 题目
&emsp;&emsp;难度系数： 1.0  
&emsp;&emsp;题目来源： Cyberpeace-n3k0  
&emsp;&emsp;题目描述：小宁写了一个登陆验证页面，随手就设了一个密码。
## 解答
&emsp;&emsp;根据题目描述应该是弱密码，尝试使用admin，admin登录失败，尝试使用admin，123456登录得到答案：`cyberpeace{e0d6f8c6f59c0934769eda6ad719b2db}`。

# simple_php
## 题目
&emsp;&emsp;难度系数： 1.0  
&emsp;&emsp;题目来源： Cyberpeace-n3k0  
&emsp;&emsp;题目描述：小宁听说php是最好的语言,于是她简单学习之后写了几行php代码。 
## 解答
&emsp;&emsp;网址访问后有如下代码。
```php
<?php
show_source(__FILE__);
include("config.php");
$a=@$_GET['a'];
$b=@$_GET['b'];
if($a==0 and $a){
    echo $flag1;
}
if(is_numeric($b)){
    exit();
}
if($b>1234){
    echo $flag2;
}
?>
```

&emsp;&emsp;根据代码逻辑，通过get方式传递a和b两个参数，其中a要为0，但不能为数字0，否则过不去and条件，所以设置为任意字母即可，b要大于1234但不能是纯数字，所以后面加一个字母。

&emsp;&emsp;访问`/?a=a&b=1235c`即可得到答案：`Cyberpeace{647E37C7627CC3E4019EC69324F66C7C}`。

# get_post
## 题目
&emsp;&emsp;难度系数： 2.0  
&emsp;&emsp;题目来源： Cyberpeace-n3k0  
&emsp;&emsp;题目描述：X老师告诉小宁同学HTTP通常使用两种请求方法，你知道是哪两种吗？
## 解答
&emsp;&emsp;访问页面获得提示`请用GET方式提交一个名为a,值为1的变量`。  
&emsp;&emsp;访问`/?a=1`得到提示:`请用GET方式提交一个名为a,值为1的变量，请再以POST方式随便提交一个名为b,值为2的变量`。

&emsp;&emsp;打开Postman，给链接`/?a=1`发送一个POST请求，body中b的值为2。

![](https://pic.lufer.cc/images/2021/08/11/image5956081436e977b6.png)

&emsp;&emsp;得到答案:`cyberpeace{7213df1a0d7ff4813ff1784115d7285c}`。

# xff_referer
## 题目
&emsp;&emsp;难度系数： 2.0  
&emsp;&emsp;题目来源： Cyberpeace-n3k0  
&emsp;&emsp;题目描述：X老师告诉小宁其实xff和referer是可以伪造的。  
## 解答
&emsp;&emsp;访问网址，提示为`ip地址必须为123.123.123.123`。  
&emsp;&emsp;用Postman访问链接，头部添加`X-Forwarded-For`，值为给定的IP地址，得到新的提示：`必须来自https://www.google.com`。

![](https://pic.lufer.cc/images/2021/08/11/image9afae6b20532fe58.png)

&emsp;&emsp;于是再添加referer，值为`https://www.google.com`。

![](https://pic.lufer.cc/images/2021/08/11/imagee8256c6ae34c615a.png)

&emsp;&emsp;得到答案：`cyberpeace{5b7a2438c6df8a7fb89edb484b2fea4d}`。 

# webshell
## 题目
&emsp;&emsp;难度系数： 2.0  
&emsp;&emsp;题目来源： Cyberpeace-n3k0  
&emsp;&emsp;题目描述：小宁百度了php一句话,觉着很有意思,并且把它放在index.php里。
## 解答
&emsp;&emsp;根据提示可以知道是WebShell攻击，用中国菜刀添加网址，得到flag.txt。打开获得答案：`cyberpeace{41e76883815baf71fba1a2e29d3e65b9}`。

# command_execution
## 题目
&emsp;&emsp;难度系数： 2.0   
&emsp;&emsp;题目来源： Cyberpeace-n3k0  
&emsp;&emsp;题目描述：小宁写了个ping功能,但没有写waf,X老师告诉她这是非常危险的，你知道为什么吗。
## 解答
&emsp;&emsp;网站只有一个ping输入框，考虑可以用ping并带其他命令的方式来执行，执行`127.0.0.1|find / -name "flag.*"`搜索服务器本地的flag文件。

>ping -c 3 127.0.0.1|find / -name "flag.*"  
/home/flag.txt

&emsp;&emsp;然后访问这个文件，`127.0.0.1|cat /home/flag.txt`，得到答案：`cyberpeace{c72bd8829fd9cab078eff060ffc63713}`。

# simple_js
## 题目
&emsp;&emsp;难度系数： 3.0  
&emsp;&emsp;题目来源： root-me  
&emsp;&emsp;题目描述：小宁发现了一个网页，但却一直输不对密码。(Flag格式为 Cyberpeace{xxxxxxxxx} )  
## 解答
&emsp;&emsp;访问之后发现需要输入密码，根据题目描述考虑可能是有js脚本，F12查看网页源码，发现如下代码：
```js

<html>
<head>
    <title>JS</title>
    <script type="text/javascript">
    function dechiffre(pass_enc){
        var pass = "70,65,85,88,32,80,65,83,83,87,79,82,68,32,72,65,72,65";
        var tab  = pass_enc.split(',');
        var tab2 = pass.split(',');
        var i,j,k,l=0,m,n,o,p = "";
        i = 0;
        j = tab.length;
        k = j + (l) + (n=0);
        n = tab2.length;
        for(i = (o=0); i < (k = j = n); i++ ){
            o = tab[i-l];p += String.fromCharCode((o = tab2[i]));
            if(i == 5)break;}
        for(i = (o=0); i < (k = j = n); i++ ){
            o = tab[i-l];
            if(i > 5 && i < k-1)
                p += String.fromCharCode((o = tab2[i]));
        }
        p += String.fromCharCode(tab2[17]);
        pass = p;return pass;
    }
    String["fromCharCode"](dechiffre("\x35\x35\x2c\x35\x36\x2c\x35\x34\x2c\x37\x39\x2c\x31\x31\x35\x2c\x36\x39\x2c\x31\x31\x34\x2c\x31\x31\x36\x2c\x31\x30\x37\x2c\x34\x39\x2c\x35\x30"));

    h = window.prompt('Enter password');
    alert( dechiffre(h) );

</script>
</head>

</html>

```

&emsp;&emsp;将后面的`\x35\x35\x2c\x35\x36\x2c\x35\x34\x2c\x37\x39\x2c\x31\x31\x35\x2c\x36\x39\x2c\x31\x31\x34\x2c\x31\x31\x36\x2c\x31\x30\x37\x2c\x34\x39\x2c\x35\x30`进行16进制到字符的转换，可以得到：`55,56,54,79,115,69,114,116,107,49,50`。  
&emsp;&emsp;转换为对应的ASCII码得到`786OsErtk12`，故答案为`Cyberpeace{786OsErtk12}`。
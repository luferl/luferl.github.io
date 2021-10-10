---
title: 自建Chevereto图床并设置邀请码注册
date: 2021-03-05 16:23:24
tags: [日常折腾,NAS]
categories: 日常折腾
---
&emsp;&emsp;之前一直在用`imgchr.com`的图床，但是近期发现无法上传图片，访问倒是正常。

&emsp;&emsp;为了防止这个图床哪天崩了，决定还是把图放在自己手里比较安全。

&emsp;&emsp;搜了一圈发现imgchr就是用chevereto搭建的，chevereto是一个开源的免费软件，那不如自己搭一个，正好搭在自己的NAS上，做个穿透即可。

# 群晖安装Chevereto

&emsp;&emsp;这里才用了什么值得买上`zhouningyi01`的教程，链接如下。但是有些许不同。

&emsp;&emsp;https://post.smzdm.com/p/a3gvxnon/

## 下载Chevereto代码

&emsp;&emsp;`https://github.com/Chevereto/Chevereto-Free`

&emsp;&emsp;选择`Download ZIP` 

## 群晖安装环境

&emsp;&emsp;在群晖的套件中心添加图中的套件，其中PHP7.2不需要手动安装，在装其他套件时会提示安装。

![需要安装的套件](https://pic.lufer.cc/images/2021/03/18/image.png)

&emsp;&emsp;打开群晖的 Web Station 套件，点击 PHP 设置，如果有就点编辑，如果没有条目就点击新增，然后选择PHP7.2，将下方的扩展名全部打勾，然后确定保存。

![PHP设置](https://pic.lufer.cc/images/2021/03/18/imagedf94afbd0485e69b.png)

&emsp;&emsp;把下载的Chevereto压缩包上传到NAS的web目录下并解压

![压缩包位置](https://pic.lufer.cc/images/2021/03/18/image845322cb34e029fb.png)

&emsp;&emsp;给Chevereto文件夹权限，`右键`-`属性`-`权限`，然后`新增`，用户组选 Everyone，并给与`管理`、`读取`、写入权限，然后勾上`应用到这个文件夹、子文件夹及文件`后保存。

![设置文件夹权限](https://pic.lufer.cc/images/2021/03/18/imagee8df02581df4b562.png)

&emsp;&emsp;打开群晖的phpMyAdmin，新建一个数据库，数据库名称可以自定义。

![新建数据库](https://pic.lufer.cc/images/2021/03/18/imagea673e78b93413800.png)

&emsp;&emsp;打开 Web Station 设置虚拟主机，根据需要选择基于名称或基于端口，因为我需要做内网穿透和HTTPS，所以选择了基于名称，这样在勾选HSTS后可以自动进行HTTP到HTTPS的跳转。如果没有这种需求可以选择基于端口。文档根目录选择到chevereto的目录，并选择对应的后端服务器和PHP版本。

![虚拟主机设置](https://pic.lufer.cc/images/2021/03/18/image5288464eb709dbca.png)

&emsp;&emsp;新建一个文本文档，将 “新建文本文档.txt” 重命名为”settings.php“之后传到 web/chevereto/app 文件夹下，缺少这一步的话打开网站会提示：Chevereto can’t create the app/settings.php file. You must manually create this file。

&emsp;&emsp;打开群晖IP地址：端口号打开管理页面然后填入数据库信息开始安装。

![数据库设置页面](https://pic.lufer.cc/images/2021/03/18/imagecb5982205d6cd52b.png)

![账号设置页面](https://pic.lufer.cc/images/2021/03/18/imagefd8aef9aa9183daa.png)

&emsp;&emsp;最后一项如果选择personal则只能自己使用，如果选择community则允许其他用户注册。

&emsp;&emsp;至此安装完成。


# 添加邀请码注册
&emsp;&emsp;修改 route.signup.php 文件，位置：`/chevereto/app/routes/route.signup.php`，找到下述代码：
```php
// Input validations
if (!filter_var($_POST['email'], FILTER_VALIDATE_EMAIL)) {
    $input_errors['email'] = _s('Invalid email');
}
if (!CHV\User::isValidUsername($_POST['username'])) {
    $input_errors['username'] = _s('Invalid username');
}
if (!preg_match('/' . CHV\getSetting('user_password_pattern') . '/', $_POST['password'])) {
    $input_errors['password'] = _s('Invalid password');
}
```
&emsp;&emsp;之后追加：
```php
//邀请码
if(!isset($_POST['invitationcode']) || $_POST['invitationcode'] != '你要设置的邀请码') {
    $input_errors['invitationcode'] = _s('Invalid invitation code');
}
```
&emsp;&emsp;修改signup.php 文件，位置：`/chevereto/app/themes/Peafowl/views/signup.php`，找到 form 表单：
```php
<form class="content-section" method="post" autocomplete="off" data-action="validate">
```
&emsp;&emsp;添加下述代码：
```php
<div class="position-relative">
    <input name="invitationcode" tabindex="1" autocomplete="off" autocorrect="off" autocapitalize="off" type="input" placeholder="<?php _se('Invitation code'); ?>" class="input animate" required value="<?php echo get_safe_post()['invitationcode']; ?>">
    <div class="text-align-left red-warning"><?php echo get_input_errors()['invitationcode']; ?></div>
</div>
```
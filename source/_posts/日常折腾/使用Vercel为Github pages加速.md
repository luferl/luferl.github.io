---
title: 使用Vercel为Github pages加速
date: 2021-11-16 11:17:52
tags: [Blog,日常折腾]
categories: 日常折腾
---
&emsp;&emsp;最近感觉Github Pages访问越来越慢了，百度了一下发现了vercel这个东西，可以自动拉取github的更新并部署，测试了一下访问速度，只能算是矮子里面拔高个，有比没有强吧。

![网速对比](https://pic.lufer.cc:8089/images/2021/11/16/image11ad8021cdfe4bad.png)

# 创建项目
&emsp;&emsp;访问vercel的官网，https://vercel.com/ ，注册账号并登陆。

&emsp;&emsp;随后选择`Add Github Org or Account`,添加账户授权。

![添加账号](https://pic.lufer.cc:8089/images/2021/11/16/image650ed8763b5b8fcf.png)

&emsp;&emsp;这里我只给了博客仓库的权限。

![仓库授权](https://pic.lufer.cc:8089/images/2021/11/16/image6b342f4861f8ac12.png)

&emsp;&emsp;然后点击`import`就可以了。

![导入仓库](https://pic.lufer.cc:8089/images/2021/11/16/image181137207cbe00d4.png)

&emsp;&emsp;注意第一步，选择跳过创建团队，否则在14天的免费试用之后要收取$20的费用。

[![不创建团队](https://pic.lufer.cc:8089/images/2021/11/16/image2271b8e17a914eb9.png)](https://pic.lufer.cc:8089/image/d2ac)

&emsp;&emsp;因为我只拉取静态页面，所以项目默认检测到Hexo是无法build出任何内容的,直接访问会404。  
&emsp;&emsp;`FRAMEWORK PRESET`改为`other`，然后把其他Build选项都override，这样就可以直接拉取静态页面并展示。

[![修改项目选项](https://pic.lufer.cc:8089/images/2021/11/16/imageb0f3c00186dc6aa3.md.png)](https://pic.lufer.cc:8089/image/dGK0)

&emsp;&emsp;点击Deploy，就会自动生成项目。

# 项目设置
&emsp;&emsp;创建好之后，还需要进行一些设置。  
## 分支设置
&emsp;&emsp;首先到`Settings`-`Git`里面，设置想要检测的分支，例如我的仓库源码分支的backup（默认分支），静态页面分支是master。所以import的时候会自动检测backup分支，我只希望拉取静态文件，故改成master分支。

[![分支设置](https://pic.lufer.cc:8089/images/2021/11/16/image8e3dce0bd14b310b.md.png)](https://pic.lufer.cc:8089/image/dLho)

## 域名设置
&emsp;&emsp;在`Settings`-`Domains`里面，输入我们自己的域名，并点击Add。

&emsp;&emsp;并根据提示，到域名的DNS管理页面将域名通过CNAME解析到`cname.vercel-dns.com`。

&emsp;&emsp;点击Refresh，就可以看到解析已经成功。

![域名解析](https://pic.lufer.cc:8089/images/2021/11/16/image90b7a33d5846b563.png)
---
title: 使用群辉的Drive套件实现同步盘
date: 2021-10-10 11:56:58
tags: [日常折腾,NAS]
categories: 日常折腾
---
&emsp;&emsp;之前一直使用OneDrive作为同步盘，用来在公司电脑、个人电脑以及pad上同步文件。

&emsp;&emsp;由于使用edu邮箱可以有有1T的空间，所以一直在用学校的邮箱作为账号，但是国庆过完之后发现怎么也无法登陆onedrive了，搜了一下居然是学校被制裁了。

&emsp;&emsp;由于我大部分工作是在公司电脑上完成的，所以公司的onedrive文件夹下基本上保有了所有的文件，连忙将文件转移出来，基本没有损失。

&emsp;&emsp;OneDrive不能用了，开始研究用自己的NAS作为同步盘，借助群辉的Drive套件。

&emsp;&emsp;Drive的官方网址：https://www.synology.cn/zh-cn/dsm/feature/drive

# 安装Drive
&emsp;&emsp;在套件中心找到`Drive`，安装套件。

&emsp;&emsp;装的时候我这边一直提示“安装套件出错”，并且装完之后在菜单里面看不见，但是看日志是已经装好的。

&emsp;&emsp;重启了一下NAS，菜单里面就出现了Drive。

![装好Drive的菜单](https://pic.lufer.cc/images/2021/10/10/image.png)

&emsp;&emsp;菜单里面会有两个新项目，`Drive管理控制台`和`Drive`。

&emsp;&emsp;其中我们主要使用的是`Drive管理控制台`，而`Drive`是一个网页版的文件查看器，并无大用。

# 配置Drive
&emsp;&emsp;首先新建一个文件夹，用于同步文件。

&emsp;&emsp;`控制面板`-`共享文件夹`，创建一个新的文件夹，我这里叫CloudSync。

&emsp;&emsp;打开`Drive管理控制台`，进入`团队文件夹`选项，把刚创建的文件夹启用。

![启用文件夹](https://pic.lufer.cc/images/2021/10/10/image345edfc2f4605009.png)

&emsp;&emsp;启用的时候会有一个对话框，全部默认点确定就行。

&emsp;&emsp;启用之后服务端的设置就已经完成了。

# FRP内网穿透
&emsp;&emsp;修改Docker里面的frpc.ini，添加一条穿透记录，采用tcp的方式穿透6690端口
```ini
[lufer_Drive]
type=tcp
local_ip=127.0.0.1
local_port=6690
remote_port=6690
custom_domains=设置的域名
```
&emsp;&emsp;随后在域名的DNS解析记录中添加上要用来解析的域名，把frpc.ini传回Docker文件夹，重启FRP服务。

# 客户端配置
&emsp;&emsp;下载Drive的Windows客户端，官网说还支持macOS，Linux，以及Android和IOS，可以说生态非常全面了。

&emsp;&emsp;http://cndl.synology.cn/download/Utility/SynologyDriveClient/1.1.4-10580/Windows/Installer/Synology%20Drive-1.1.4-10580.exe?SynoToken=HSoLkkUiP9JSk

&emsp;&emsp;下载完成之后安装，输入域名及登录群辉的用户名和密码，选择文件夹。

&emsp;&emsp;这里借用了别人的图，因为我已经设置过了，先点铅笔，选择Drive中的文件夹，再配置本地文件夹，然后下一步即可。

![文件夹设置](https://pic.lufer.cc/images/2021/10/10/imagedb2ac653df8692ee.png)

&emsp;&emsp;下一步有一个共享盘，这个没什么用，跳过就行，然后就完成了配置。

# 使用效果
&emsp;&emsp;完成之后在你配置的本地文件夹内，如果你规则选择的是双向同步（默认），那么文件夹内所有的更改都会同步到NAS上，和OneDrive的使用效果相同。

&emsp;&emsp;实际用起来速度还是很快的。

![任务同步](https://pic.lufer.cc/images/2021/10/10/16338399341.png)
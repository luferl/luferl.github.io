---
title: 借助Aria2和Chrome插件实现NAS远程一键下载
date: 2021-04-06 09:52:44
tags: [日常折腾,NAS]
categories: 日常折腾
---
# Docker安装Aria2
&emsp;&emsp;选择`aria2-with-webui`。

![aria2-with-webui](https://pic.lufer.cc/images/2021/04/06/image.png)

&emsp;&emsp;将要存放下载文件的路径映射到`data`目录，并准备文件夹映射到`conf`目录。

![卷映射](https://pic.lufer.cc/images/2021/04/06/image7f0411d8a13fce84.png)

&emsp;&emsp;自定义`80`和`8080`对应的本地端口。

![修改端口](https://pic.lufer.cc/images/2021/04/06/image1f514ee89f06b09e.png)

&emsp;&emsp;在环境变量中添加一个`rpc-secret`，自定义令牌密码。

![自定义令牌密码](https://pic.lufer.cc/images/2021/04/06/imagea1c5a07d88e1da48.png)

&emsp;&emsp;然后启动容器。

# FRP穿透
&emsp;&emsp;修改frpc.ini，把之前设置的80对应的本地端口以及6800端口映射出去。  
&emsp;&emsp;我之前设置的是7001对应80端口，所以穿透7001，便于网络访问。  
&emsp;&emsp;把6800端口穿透出去才能够远程创建下载任务。
```ini
[lufer_aria]
type=http
local_ip=127.0.0.1
local_port=7001
custom_domains= 你的域名

[lufer_ariarpc]
type=tcp
local_ip=127.0.0.1
local_port=6800
remote_port=6800
custom_domains= 你的域名
```
&emsp;&emsp;设置好后重启frp容器。

# Chrome插件
&emsp;&emsp;Chrome安装插件`Aria2 for Chrome`。

&emsp;&emsp;https://chrome.google.com/webstore/detail/aria2-for-chrome/mpkodccbngfoacfalldjimigbofkhgjn

&emsp;&emsp;装好之后打开设置页面。

&emsp;&emsp;把下载拦截的第一项关掉，否则所有任务都会发送到NAS上。

&emsp;&emsp;RPC Server处设置好令牌密码和rpc地址，点击保存即可。

![插件设置](https://pic.lufer.cc/images/2021/04/06/image9a46db3243c2a71a.png)

# 网页端设置

&emsp;&emsp;访问穿透出去的域名，打开aria2的管理页面。  
&emsp;&emsp;打开`设置`-`连接设置`。

![连接设置](https://pic.lufer.cc/images/2021/04/06/image61ca82970fb51152.png)

&emsp;&emsp;主机和RPC路径应该都是自动填好的，只需要设置好密码令牌即可。

![设置密码令牌](https://pic.lufer.cc/images/2021/04/06/image65d6514f44bf554b.png)

&emsp;&emsp;保存即可完成配置，右侧会提示连接成功。

![配置成功提示](https://pic.lufer.cc/images/2021/04/06/image68bf77b1d4f6b27c.png)

# 使用
&emsp;&emsp;在需要下载到NAS的链接上点击右键，选择`导出到ARIA2 RPC`即可。

![一键远程下载](https://pic.lufer.cc/images/2021/04/06/image56c461c9d5fd48d6.png)

&emsp;&emsp;如果需要下载磁力或种子，可打开管理页面，手动添加。

![下载磁链或种子](https://pic.lufer.cc/images/2021/04/06/imagedf3b0adde1f3e8c7.png)
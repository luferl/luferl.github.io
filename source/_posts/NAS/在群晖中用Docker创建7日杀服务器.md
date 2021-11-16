---
title: 在群晖中用Docker创建7日杀服务器
date: 2021-11-16 10:41:28
tags: [日常折腾,NAS]
categories: 日常折腾
---
# 选择映像
&emsp;&emsp;在docker的注册表中搜索7dtd，下载didstopia的这个映像即可。

[![docker市场](https://pic.lufer.cc:8089/images/2021/11/16/image8d24a9227f248b50.md.png)](https://pic.lufer.cc:8089/image/dliT)

&emsp;&emsp;此映像的官方文档如下：

&emsp;&emsp;https://registry.hub.docker.com/r/didstopia/7dtd-server/

# 配置容器
## 资源限制
&emsp;&emsp;这个映像大小是1GB，下载完成之后启动。  
&emsp;&emsp;给映像分配不低于4096MB的内存，不然资源可能不够用。

[![资源限制](https://pic.lufer.cc:8089/images/2021/11/04/image.md.png)](https://pic.lufer.cc:8089/image/dE25)

## 文件夹映射
&emsp;&emsp;在系统中创建两个文件夹，分别用于存放steamcmd与7dtd delicated server以及服务器配置文件。

&emsp;&emsp;我这里创建了data文件夹用于存放steam及服务器程序，config文件夹用于存放服务器配置文件及存档。

![准备文件夹](https://pic.lufer.cc:8089/images/2021/11/16/imagef396358ddc36f5ad.png)

&emsp;&emsp;准备好两个文件夹之后在docker中创建映射。  
&emsp;&emsp;分别映射到`/app/.local/share/7DaysToDie`和`/steamcmd/7dtd`

[![文件映射](https://pic.lufer.cc:8089/images/2021/11/04/image491f728efd1445cd.png)](https://pic.lufer.cc:8089/image/dQdv)

## 端口映射
&emsp;&emsp;七日杀服务器默认使用的端口是26900~26902，然后8080和8081分别用来启用管理员网页后台以及telnet端口，按图中设置即可。

[![端口映射](https://pic.lufer.cc:8089/images/2021/11/04/imageeea269dd233508b5.png)](https://pic.lufer.cc:8089/image/dZMy)

# 服务器配置
## 修改docker启动方式
&emsp;&emsp;首先启动一次docker，会自动下载最新的steamcmd和七日杀服务器程序。  
&emsp;&emsp;但是每次docker启动时都会自动下载，所以在下载成功一次之后我们可以改一次docker配置，在docker的环境变量里面把`SEVEN_DAYS_TO_DIE_START_MODE`改为2，默认为0。0代表每次都自动下载最新版，1代表只更新，2代表跳过更新直接启动。

![修改启动模式](https://pic.lufer.cc:8089/images/2021/11/16/image4e7387ef23d139a6.png)

## 修改服务器配置
&emsp;&emsp;找到我们之前创建的config文件夹，下载其中的serverconfig.xml，可以修改服务器密码，服务器所使用的存档以及一些游戏性设置，具体可见官方说明。

&emsp;&emsp;如果有先前的存档，可以上传至config\Saves\对应的文件夹下，然后修改serverconfig.xml把word改成对应的存档文件夹名称即可。
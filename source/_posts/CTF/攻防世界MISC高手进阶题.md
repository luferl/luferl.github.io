---
title: 攻防世界MISC高手进阶题
date: 2021-08-12 17:07:52
tags: [CTF,MISC]
categories: CTF
---
# reverseMe
## 题目
&emsp;&emsp;难度系数： 1.0  
&emsp;&emsp;题目来源： XCTF 3rd-GCTF-2017
&emsp;&emsp;题目描述：暂无
&emsp;&emsp;题目场景： 暂无
## 解答
&emsp;&emsp;把附件图镜像之后得到答案。

![](https://pic.lufer.cc:8089/images/2021/08/12/imagea71a2155963c06c2.png)

# base64÷4
## 题目
&emsp;&emsp;难度系数： 1.0  
&emsp;&emsp;题目来源： 暂无  
&emsp;&emsp;题目描述：暂无  
## 解密
&emsp;&emsp;看题目以为是先*4或者/4之后进行base64解密，发现怎么都不对，后来考虑十六进制直接转字符串，得到答案：`

# embarrass
## 题目
&emsp;&emsp;难度系数： 1.0  
&emsp;&emsp;题目来源： ciscn-2017   
&emsp;&emsp;题目描述：暂无  
## 解答
&emsp;&emsp;给了一个pcapng，用wireshark打开搜了半天flag也没找到什么内容。  
&emsp;&emsp;百度了一下，发现直接检索flag就可以，确实很embarrass。

![](https://pic.lufer.cc:8089/images/2021/08/12/image7c4fd1595a4f268b.png)

# 神奇的Modbus
## 题目
&emsp;&emsp;难度系数： 1.0  
&emsp;&emsp;题目来源： XCTF 4th-SCTF-2018  
&emsp;&emsp;题目描述：寻找flag,提交格式为sctf{xxx}  
## 解答
&emsp;&emsp;附件是一个抓包文件，根据题目提示，关注modbus类型的协议，随便找一条追踪tcp流，发现答案。

![](https://pic.lufer.cc:8089/images/2021/08/12/image02b1e98d656e284f.png)

&emsp;&emsp;但是Easy_Mdbus过不了，要提交Easy_Modbus才可以。

# something_in_image
## 题目
&emsp;&emsp;难度系数： 1.0  
&emsp;&emsp;题目来源： 2019湖湘杯  
&emsp;&emsp;题目描述：暂无
## 解答
&emsp;&emsp;我搁这解压缩半天，找到了一个congratulations2文件夹，激动半天发现往下走不动了，百度一下发现人家strings一下就搜出来了。

![](https://pic.lufer.cc:8089/images/2021/08/12/image00a34d642dbcd955.png)

# wireshark-1
## 题目
&emsp;&emsp;难度系数： 1.0  
&emsp;&emsp;题目来源： 广西首届网络安全选拔赛  
&emsp;&emsp;题目描述：黑客通过wireshark抓到管理员登陆网站的一段流量包（管理员的密码即是答案)。 flag提交形式为flag{XXXX}
## 解答 
&emsp;&emsp;打开流量包，检索login，找到用户登录的password。

![](https://pic.lufer.cc:8089/images/2021/08/12/image307b4085e0e9e0e3.png)

# pure_color
## 题目
&emsp;&emsp;难度系数： 1.0  
&emsp;&emsp;题目来源： school-ctf-winter-2015  
&emsp;&emsp;题目描述：格式为flag{xxxxxx}  
## 解答
&emsp;&emsp;用StegSolve打开附件，切换通道，得到flag:`true_steganographers_doesnt_need_any_tools`。

[![](https://pic.lufer.cc:8089/images/2021/08/13/image.md.png)](https://pic.lufer.cc:8089/image/dqBK)
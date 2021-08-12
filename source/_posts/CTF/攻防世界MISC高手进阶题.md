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

![imagea71a2155963c06c2.png](https://pic.lufer.cc/images/2021/08/12/imagea71a2155963c06c2.png)

# base64÷4
## 题目
&emsp;&emsp;难度系数： 1.0  
&emsp;&emsp;题目来源： 暂无  
&emsp;&emsp;题目描述：暂无  
## 解密
&emsp;&emsp;看题目以为是先*4或者/4之后进行base64解密，发现怎么都不对，后来考虑十六进制直接转字符串，得到答案：`flag{E33B7FD8A3B841CA9699EDDBA24B60AA}`。
---
title: CFT选拔赛题解
date: 2021-08-13 15:46:20
tags: [CTF]
categories: CTF
---
# PWN
# Crypto
## 基础题--签到
### 题目
&emsp;&emsp;U2FuZ2ZvcntXZUxjME1lX1QwX1Nhbmdmb3JfQ1RGfQ==  
&emsp;&emsp;提交格式为：sangfor{xxxxxxx}
### 解答
&emsp;&emsp;Base64解码得到答案：`Sangfor{WeLc0Me_T0_Sangfor_CTF}`，注意根据提示，第一个S要换成小写字母。

## 简单的凯撒+base64
### 题目
&emsp;&emsp;d2Vya2pzdntteEBfbXdfeml2OV9pQHdjfQ==  
&emsp;&emsp;位移：4   
&emsp;&emsp;Flag提交格式：sangfor{xxxxxxx}
### 解答
&emsp;&emsp;先Base64解码，得到：`werkjsv{mx@_mw_ziv9_i@wc}`。    
&emsp;&emsp;再根据提示，用位移为4的凯撒密码解码，得到答案：`sangfor{it@_is_ver9_e@sy}`。

## 有趣的密文
### 题目
&emsp;&emsp;小啊giao在书上看见了一段密文： asfngrof{gla@esin@y}b   
&emsp;&emsp;然后密文旁边的注释凌乱的写着：2153476   
&emsp;&emsp;聪明的你能否帮助小啊giao破解出密文获得flag吗？
### 解答
&emsp;&emsp;当时我是手动置换的，这里有在线网站:
https://ctftools.com/down/down/passwd/

&emsp;&emsp;使用其中的置换密码功能，输入排列和密文得到答案：`sangfor{flage@is@ynb}`。 

## Affine
### 题目
&emsp;&emsp;y=25x-6 密文：cuhopgdwht   
&emsp;&emsp;Flag提交格式：sangfor{xxxxxxxx}
### 解答
&emsp;&emsp;使用Affine解码脚本：
```python
s = 'cuhopgdwht'
s1 = ''
len = len(s)
for i in range(0, len):
    //系数根据图标对应得到，后面反向加减
    a = (25 * (ord(s[i]) - 97 + 6)) % 26
    s1 += chr(a + 97)
print(s1)
```
&emsp;&emsp;其中计算部分系数使用下图，本题函数系数25，采用25的逆元，还是25。

![](https://pic.lufer.cc:8089/images/2021/08/13/imagea466b9588dea63a3.png)

&emsp;&emsp;答案：`sangfor{sangforynb}`

## Base64的亲戚
### 题目
&emsp;&emsp;:A:?TqXusB?aW}%pD8j{So[tJ.l@?nRcBr/4P}^dt?ok)wO_?;:{]I-<KYj-q#d96v2;]=UF/GPV+k%mF%$5^h+#s(YoiJX)MEE5eQ7MW9m$kDM/LzPupv2vJai]B#R}8TFo[xc)syWXB4?0-^taieX6E=vyo/+X8Y=1sX2$.}O}<wIlE_k/Bg3:J0y!U}woK7:
### 解答
&emsp;&emsp;用Basecrack解密：
```
[>] Enter Encoded Base::A:?TqXusB?aW}%pD8j{So[tJ.l@?nRcBr/4P}^dt?ok)wO_?;:{]I-<KYj-q#d96v2;]=UF/GPV+k%mF%$5^h+#s(YoiJX)MEE5eQ7MW9m$kDM/LzPupv2vJai]B#R}8TFo[xc)syWXB4?0-^taieX6E=vyo/+X8Y=1sX2$.}O}<wIlE_k/Bg3:J0y!U}woK7:

[>] Decoding as Base92: E:)d)8NH*6f!^afecoIG"hESQP]y,aiY^tm0Z0<SB8*@@7ee#ww2;yrj)$RbB8oa[fx2k23N;Og!S9{c!/Jz)wiC7OVz,+7d`7;dul1j@#F)1l~cL5nJ]!/BrI4fFw_b#i@Jj9L["OAe2N&eviWHb7#zJO~(uC

[-] The Encoding Scheme Is Base92
```
&emsp;&emsp;得到用Base92解密之后的字符串，再次解密：
```
[>] Enter Encoded Base: E:)d)8NH*6f!^afecoIG"hESQP]y,aiY^tm0Z0<SB8*@@7ee#ww2;yrj)$RbB8oa[fx2k23N;Og!S9{c!/Jz)wiC7OVz,+7d`7;dul1j@#F)1l~cL5nJ]!/BrI4fFw_b#i@Jj9L["OAe2N&eviWHb7#zJO~(uC

[>] Decoding as Base91: RzRaVE1NSldJVTNET05SV0daRERPTVJYSUkyREVOQlFHNFpUSU5KVklZMkRTTlpUR1ZERElPSldJVTNUSU5SVkc0WkRNTkpYR00zVElOUlpHWkNUTU5aWElRPT09PT09

[-] The Encoding Scheme Is Base91
```
&emsp;&emsp;得到用Base91解密之后的字符串，再次解密。
```
[>] Enter Encoded Base: RzRaVE1NSldJVTNET05SV0daRERPTVJYSUkyREVOQlFHNFpUSU5KVklZMkRTTlpUR1ZERElPSldJVTNUSU5SVkc0WkRNTkpYR00zVElOUlpHWkNUTU5aWElRPT09PT09

[>] Decoding as Base64: G4ZTMMJWIU3DONRWGZDDOMRXII2DENBQG4ZTINJVIY2DSNZTGVDDIOJWIU3TINRVG4ZDMNJXGM3TINRZGZCTMNZXIQ======

[-] The Encoding Scheme Is Base64
```
&emsp;&emsp;得到用Base64解密之后的字符串，再次解密：
```
[>] Enter Encoded Base: G4ZTMMJWIU3DONRWGZDDOMRXII2DENBQG4ZTINJVIY2DSNZTGVDDIOJWIU3TINRVG4ZDMNJXGM3TINRZGZCTMNZXIQ======

[>] Decoding as Base32: 73616E67666F727B424073455F49735F496E746572657374696E677D

[-] The Encoding Scheme Is Base32
```
&emsp;&emsp;得到用Base32解密的字符串，再次解密：
```
[>] Enter Encoded Base: m73616E67666F727B424073455F49735F496E746572657374696E677D

[>] Decoding as Base16: sangfor{B@sE_Is_Interesting}

[-] The Encoding Scheme Is Base16
```
&emsp;&emsp;得到用Base16解密的字符串，即为答案。

## twoTree
### 题目
&emsp;&emsp;Hint: Front？ middle？ back？Which is correct? I think it's behind.  
&emsp;&emsp;Flag提交格式:sangfor{xxxxxxx}
### 解答
&emsp;&emsp;题目附件是一张打不开图片，根据提示可能图的前中后有信息，用Winhex打开，发现图片首位全部是十六进制数，复制出来并转为文本得到两个字符串：
```
f09e54c1bad2x38mvyg7wzlsuhkijnop
905e4c1fax328mdyvg7wbsuhklijznop
```
&emsp;&emsp;根据提示和两个字符串的构造，应该是二叉树的前序遍历和中序遍历，后序遍历即为答案。
借助python实现脚本：
```python
def last_sort(str1, str2):
    if len(str2) <= 1:
        return str2
    else:
        return last_sort(str1[1:str2.index(str1[0]) + 1], str2[:str2.index(str1[0])]) + last_sort(
            str1[str2.index(str1[0]) + 1:],
            str2[str2.index(str1[0]) + 1:
            ]) + str1[0:1]


str1 = ['f', '0', '9', 'e', '5', '4', 'c', '1', 'b', 'a', 'd', '2', 'x', '3', '8', 'm', 'v', 'y', 'g', '7', 'w', 'z',
        'l', 's', 'u', 'h', 'k', 'i', 'j', 'n', 'o', 'p']
str2 = ['9', '0', '5', 'e', '4', 'c', '1', 'f', 'a', 'x', '3', '2', '8', 'm', 'd', 'y', 'v', 'g', '7', 'w', 'b', 's',
        'u', 'h', 'k', 'l', 'i', 'j', 'z', 'n', 'o', 'p']
print(last_sort(str1, str2))
```
&emsp;&emsp;得到后序遍历为`951c4e03xm82yw7gvdakhusjilponzbf`。
# Web
## web1
### 题目
&emsp;&emsp;key会在哪里呢？

http://sangforctfweb2.free.idcfengye.com/web1.html
### 解答
&emsp;&emsp;访问目标网址，F12看网页源码，得到答案：`sangfor{flag_admiaanaaaaaaaaaaa}`。

# 杂项
## 签到
### 题目
&emsp;&emsp;这题很简单，../-  
&emsp;&emsp;Flag提交格式:sangfor{xxxxx}
### 解答
&emsp;&emsp;附件是莫斯密码：
```
.../.-/-./--./..-./---/.-./----.--/.--/...--/.-../-.-./-----/--/./..--.-/-/-----/..--.-/-.-./.-./-.--/.--./-/-----/-----.-
```
&emsp;&emsp;解密获得答案：`sangfor{w3lc0met0crypt0}`。
## 漂亮小姐姐
### 题目
&emsp;&emsp;漂亮小姐姐说了要学会百度来解密，解密的钥匙：sangfor  
&emsp;&emsp;Flag提交格式:sangfor{xxxxxxxx}
### 解答
&emsp;&emsp;根据提示，百度搜索图片解密，找到网站http://www.jsons.cn/imghideinfo/

&emsp;&emsp;上传图片并填入密码`sangfor`，得到答案`sangfor{You_@re_So_Clever}`。 

## fake encryption
### 题目
&emsp;&emsp;提交格式为：sangfor{xxxxxxx}  
&emsp;&emsp;hint: 总有马大哈会把登陆密码泄露出去
### 解答
&emsp;&emsp;根据提示，在附件的抓包里面寻找password，找到记录之后追踪TCP流。

![](https://pic.lufer.cc:8089/images/2021/08/17/image.png)

&emsp;&emsp;用找到的Password作为密码解压附件中的压缩包，得到答案`sangfor{hiahiahiahiathisistheflag}`。
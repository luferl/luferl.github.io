---
title: 攻防世界MISC新手练习题
date: 2021-08-10 09:22:20
tags: [CTF]
categories: CTF
---
# this_is_flag 
## 题目
&emsp;&emsp;难度系数： 2.0  
&emsp;&emsp;题目来源： 暂无  
&emsp;&emsp;题目描述：Most flags are in the form flag{xxx}, for example:flag{th1s_!s_a_d4m0_4la9}  
&emsp;&emsp;题目场景： 暂无  
&emsp;&emsp;题目附件： 暂无  

## 解答
&emsp;&emsp;样例题，直接复制题目中给出的`flag{th1s_!s_a_d4m0_4la9}`。

# pdf
## 题目
&emsp;&emsp;难度系数： 3.0  
&emsp;&emsp;题目来源： csaw  
&emsp;&emsp;题目描述：菜猫给了菜狗一张图，说图下面什么都没有  
&emsp;&emsp;题目场景： 暂无  
## 解答
&emsp;&emsp;题目提示是图下面什么都没有，直接打开pdf并全选复制，可得到图下面的字符串`flag{security_through_obscurity}`

# 如来十三掌
## 题目
&emsp;&emsp;难度系数： 3.0  
&emsp;&emsp;题目来源： 暂无  
&emsp;&emsp;题目描述：菜狗为了打败菜猫，学了一套如来十三掌。  
&emsp;&emsp;题目场景： 暂无  
## 解答
&emsp;&emsp;题目附件是一个word，打开之后这段文字可以联想到佛语加密，在前面加上`佛曰：`，然后用佛曰解密。

https://www.keyfc.net/bbs/tools/tudoucode.aspx

&emsp;&emsp;可得到字符串：`MzkuM3gvMUAwnzuvn3cgozMlMTuvqzAenJchMUAeqzWenzEmLJW9`。

&emsp;&emsp;联系题目提示“如来十三掌”，再用rot13解密，得到字符串：`ZmxhZ3tiZHNjamhia3ptbmZyZGhidmNraWpuZHNrdmJramRzYWJ9`。

&emsp;&emsp;最后用Base64解码，得到flag：`flag{bdscjhbkzmnfrdhbvckijndskvbkjdsab}`。

# give_you_flag
## 题目
&emsp;&emsp;难度系数： 4.0  
&emsp;&emsp;题目来源： 暂无  
&emsp;&emsp;题目描述：菜狗找到了文件中的彩蛋很开心，给菜猫发了个表情包  
&emsp;&emsp;题目场景： 暂无
## 解答
&emsp;&emsp;观察题目附件给出的gif，可以看到闪过一个二维码，将其截取出来。

![image19c2bb7b4dddc35a.png](https://pic.lufer.cc/images/2021/08/10/image19c2bb7b4dddc35a.png)

&emsp;&emsp;这张图缺失了三个定位点，手动画一个之后扫描识别可以得到flag。

![imagefda1a35bd985ef02.png](https://pic.lufer.cc/images/2021/08/10/imagefda1a35bd985ef02.png)

&emsp;&emsp;`flag{e7d478cf6b915f50ab1277f78502a2c5}`

# stegano
## 题目
&emsp;&emsp;难度系数： 4.0  
&emsp;&emsp;题目来源： CONFidence-DS-CTF-Teaser  
&emsp;&emsp;题目描述：菜狗收到了图后很开心，玩起了pdf 提交格式为flag{xxx}，解密字符需小写  
&emsp;&emsp;题目场景： 暂无  
## 解答
&emsp;&emsp;打开PDF，全选复制查看是否有隐藏内容，发现可得到如下字符串。
>NoFlagHere! NoFlagHere! NoFlagHere! XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX Close - but still not here !
BABA BBB BA BBA ABA AB B AAB ABAA AB B AA BBB BA AAA BBAABB AABA ABAA AB BBA BBBAAA ABBBB BA AAAB ABBBB AAAAA ABBBB BAAA ABAA AAABB BB AAABB AAAAA AAAAA AAAAB BBA AAABB

&emsp;&emsp;用_替换B，用.替换A，得到字符串：  
>--..-- ..-. .-.. .- --. ---... .---- -. ...- .---- ..... .---- -... .-.. ...-- -- ...-- ..... ..... ....- --. ...--

&emsp;&emsp;解码字符串得到答案：`flag{1nv151bl3m3554g3}`
# 坚持60s
## 题目
&emsp;&emsp;难度系数： 4.0  
&emsp;&emsp;题目来源： 08067CTF  
&emsp;&emsp;题目描述：菜狗发现最近菜猫不爱理他，反而迷上了菜鸡  
&emsp;&emsp;题目场景： 暂无  
## 解答
&emsp;&emsp;附件是一个jar包，考虑用反编译工具进行逆向。  
&emsp;&emsp;在Idea中打开jar包，定位到`cn.bjsxt\plane\PlaneGameFrame.class`,可以看到如下代码
```java
    case 4:
        this.printInfo(g, "加油你就是下一个老王", 50, 150, 300);
        break;
    case 5:
        this.printInfo(g, "如果撑过一分钟我岂不是很没面子", 40, 30, 300);
        break;
    case 6:
        this.printInfo(g, "flag{RGFqaURhbGlfSmlud2FuQ2hpamk=}", 50, 150, 300);
```
&emsp;&emsp;发现flag字符串结尾有个`=`，考虑是用base64加密过的，将`RGFqaURhbGlfSmlud2FuQ2hpamk=`解密后得到`DajiDali_JinwanChiji`，所以答案为`flag{DajiDali_JinwanChiji}`。
# gif
## 题目
&emsp;&emsp;难度系数： 4.0  
&emsp;&emsp;题目来源： 暂无  
&emsp;&emsp;题目描述：菜狗截获了一张菜鸡发给菜猫的动态图，却发现另有玄机  
&emsp;&emsp;题目场景： 暂无  
## 解答
&emsp;&emsp;打开附件发现是由黑白两种颜色的图构成，考虑是用二进制表示的ASCII码，共有104张图，而ASCII码的二进制为8位数，故将文件排列成13*8的矩阵排列，根据每一行八张图的黑白，用白色代表0，黑色代表1，得到二进制序列。  
>01100110 01101100 01100001 01100111 01111011 01000110 01110101 01001110 01011111 01100111 01101001 01000110 01111101 01111101

&emsp;&emsp;转为ASCII码得到答案：`flag{FuN_giF}`。

# 掀桌子
&emsp;&emsp;难度系数： 4.0  
&emsp;&emsp;题目来源： DDCTF2018   
&emsp;&emsp;题目描述：菜狗截获了一份报文如下c8e9aca0c6f2e5f3e8c4efe7a1a0d4e8e5a0e6ece1e7a0e9f3baa0e8eafae3f9e4eafae2eae4e3eaebfaebe3f5e7e9f3e4e3e8eaf9eaf3e2e4e6f2，生气地掀翻了桌子(╯°□°）╯︵ ┻━┻  
&emsp;&emsp;题目场景： 暂无  
&emsp;&emsp;题目附件： 暂无  
## 解答
&emsp;&emsp;题目没有附件，就只能从题干字符串得到答案，观察题干字符串可能是16进制数，将字符串两个字符一组，作为16进制数转换为10进制。

&emsp;&emsp;将10进制数减去128后再转换为ASCII码，得到答案：
`flag{hjzcydjzbjdcjkzkcugisdchjyjsbdfr}`

# ext3
## 题目
&emsp;&emsp;难度系数： 5.0  
&emsp;&emsp;题目来源： bugku  
&emsp;&emsp;题目描述：今天是菜狗的生日，他收到了一个linux系统光盘  
&emsp;&emsp;题目场景： 暂无  
## 解答
&emsp;&emsp;先用Winhex打开附件，搜索flag，可以找到如下内容。

![imagef70387b3841742c8.png](https://pic.lufer.cc/images/2021/08/10/imagef70387b3841742c8.png)

&emsp;&emsp;将后缀名改为zip之后解压，找到`O7avZhikgKgbF\flag.txt`，打开之后发现字符串为`ZmxhZ3tzYWpiY2lienNrampjbmJoc2J2Y2pianN6Y3N6Ymt6an0=`，用base64解码得到答案：`flag{sajbcibzskjjcnbhsbvcjbjszcszbkzj}`。

# SimpleRAR
## 题目
&emsp;&emsp;难度系数： 5.0  
&emsp;&emsp;题目来源： 08067CTF  
&emsp;&emsp;题目描述：菜狗最近学会了拼图，这是他刚拼好的，可是却搞错了一块(ps:双图层)  
&emsp;&emsp;题目场景： 暂无  
## 解答
&emsp;&emsp;用Winhex打开文件，发现flag.txt后藏了一个secret.png。

![imaged1d57f8656659cf0.png](https://pic.lufer.cc/images/2021/08/10/imaged1d57f8656659cf0.png)

> HEAD_TYPE=0x72 标记块  
    HEAD_TYPE=0x73 压缩文件头  
    HEAD_TYPE=0x74 文件头  
    HEAD_TYPE=0x75 注释头  
    HEAD_TYPE=0x76 旧风格的用户身份信息  
    HEAD_TYPE=0x77 子块  
    HEAD_TYPE=0x78 恢复纪录  
    HEAD_TYPE=0x79 用户身份信息  
    HEAD_TYPE=0x7a subblock  

&emsp;&emsp;根据rar文件格式，将标记处的7A改为文件头的标志74，保存后解压文件，得到secret.png。

&emsp;&emsp;而secret.png是一个纯白图片，继续用Winhex打开，发现其文件头为`GIF89a`，考虑这是一个gif文件。

&emsp;&emsp;根据题目提示双图层，用PS打开，每个图层分别保存为gif文件。   

&emsp;&emsp;用StegSolve打开每个gif，可以得到两个拼接的图片。

![image.png](https://pic.lufer.cc/images/2021/08/11/image.png)

![imagefb6a4a597307f904.png](https://pic.lufer.cc/images/2021/08/11/imagefb6a4a597307f904.png)

&emsp;&emsp;将两个图片拼接，补全定位点，得到最终的二维码。

![imageccebd2ad4fd981b8.png](https://pic.lufer.cc/images/2021/08/11/imageccebd2ad4fd981b8.png)

&emsp;&emsp;扫描后得到答案：`flag{yanji4n_bu_we1shi}`。
# base64stego
## 题目
&emsp;&emsp;难度系数： 5.0  
&emsp;&emsp;题目来源： olympicCTF  
&emsp;&emsp;题目描述：菜狗经过几天的学习，终于发现了如来十三掌最后一步的精髓  
&emsp;&emsp;题目场景： 暂无  
## 解答
&emsp;&emsp;根据题目名称，可以想到这是一道隐写题目，附件下载之后是个zip，但是解压需要密码，考虑是伪加密。

&emsp;&emsp;用Winhex打开zip文件，搜索504B，可以找到结果如下。

![image2b8d97fb9733f5be.png](https://pic.lufer.cc/images/2021/08/10/image2b8d97fb9733f5be.png)

&emsp;&emsp;根据zip文件格式：

>压缩源文件目录区：   
50 4B 01 02：目录中文件文件头标记(0x02014b50)   
3F 00：压缩使用的 pkware 版本  
14 00：解压文件所需 pkware 版本   
00 00：全局方式位标记（有无加密，伪加密的关键）

&emsp;&emsp;可知将`3F031403`后的`0900`改为`0000`可以解除伪加密，修改之后保存文件，得到`stego.txt`。

&emsp;&emsp;阅读stego的内容可发现是base64字符串，联系题干的base64隐写，借助脚本解密内容可以得到答案，脚本如下：
```python
import base64

b64chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/'
with open('stego.txt', 'rb') as f:
    flag = ''
    bin_str = ''
    for line in f.readlines():
        stegb64 = str(line, "utf-8").strip("\n")
        rowb64 = str(base64.b64encode(base64.b64decode(stegb64)), "utf-8").strip("\n")
        offset = abs(b64chars.index(stegb64.replace('=', '')[-1]) - b64chars.index(rowb64.replace('=', '')[-1]))
        equalnum = stegb64.count('=')  # no equalnum no offset
        if equalnum:
            bin_str += bin(offset)[2:].zfill(equalnum * 2)
        print([chr(int(bin_str[i:i + 8], 2)) for i in range(0, len(bin_str), 8)])
```
&emsp;&emsp;得到的结果为`Base_sixty_four_point_five`，用`flag{}`套起来就是答案。
# 功夫再高也怕菜刀
## 题目
&emsp;&emsp;难度系数： 6.0  
&emsp;&emsp;题目来源： 安恒杯  
&emsp;&emsp;题目描述：菜狗决定用菜刀和菜鸡决一死战  
&emsp;&emsp;题目场景： 暂无  
## 解答
&emsp;&emsp;题目附件给了一个.pcapng文件，是网络流量包文件，用Wireshark打开。

&emsp;&emsp;在分组字节流中查找flag，可以检索到1150行有`flag.txt`字样。

![image.png](https://pic.lufer.cc/images/2021/08/10/image.png)

&emsp;&emsp;观察报文内容可知这里有一个jpg文件，追踪TCP流，可以看到有FFD8开头的字符串，找到FFD9结尾，并复制出来。

&emsp;&emsp;这里会找到两个FFD8，但是第一个无法解析，要用后面那个长一点的。

![image860b328bb1e7352e.png](https://pic.lufer.cc/images/2021/08/10/image860b328bb1e7352e.png)

&emsp;&emsp;另存为jpg文件，可以得到图片。

![imageea60dd5b24316708.png](https://pic.lufer.cc/images/2021/08/10/imageea60dd5b24316708.png)

&emsp;&emsp;可以得到一个密码`Th1s_1s_p4sswd_!!!`。

&emsp;&emsp;继续检索`flag.txt`,可以在1367行找到一段内容。

![image78c95be7ac245787.png](https://pic.lufer.cc/images/2021/08/10/image78c95be7ac245787.png)

&emsp;&emsp;考虑这里是一个压缩文件，将`->|`到`|<-`之间的内容复制出来，用Winhex保存为zip文件。

![image5d8f4ebba04021cc.png](https://pic.lufer.cc/images/2021/08/10/image5d8f4ebba04021cc.png)

&emsp;&emsp;将压缩文件解压，发现需要密码，使用先前得到的密码，得到flag.txt,从而得到答案：`flag{3OpWdJ-JP6FzK-koCMAK-VkfWBq-75Un2z}`。

## 补充
&emsp;&emsp;将pcapng直接改名为zip文件，用360压缩可以直接打开。

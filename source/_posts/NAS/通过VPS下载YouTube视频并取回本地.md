---
title: 通过VPS下载YouTube视频并取回本地
date: 2021-09-13 16:51:46
tags: [日常折腾,NAS]
categories: 日常折腾
---
&emsp;&emsp;最近想看某个电视剧，逛了一圈发现国内的版权方免费仅能看两集，且最高为1080P，但是在YouTube上可以直接看，并且支持4K的分辨率，吃相太难看了！

&emsp;&emsp;但是由于4K的分辨率文件太大了，如果借助魔法工具流量吃不消，正好手上有国外VPS，拿来作为一个下载的中转岂不美哉。

# youtube-dl
&emsp;&emsp;youtube-dl是一个基于python的youtube下载工具，官网：https://github.com/ytdl-org/youtube-dl

安装只需执行如下脚本：
```
wget https://yt-dl.org/downloads/latest/youtube-dl -O /usr/local/bin/youtube-dl
chmod a+rx /usr/local/bin/youtube-dl
```

&emsp;&emsp;安装之后就可以通过`youtube-dl`命令来执行下载。

&emsp;&emsp;如果想下载4K清晰度的视频，需要先检测链接中包含的视频。  
&emsp;&emsp;通过`youtube -F [url]`来嗅探指定url下面的视频内容。
```
root@p1614135807:/usr/bin# youtube-dl -F https://www.youtube.com/watch?v=7V_XMfO89j0
[youtube] 7V_XMfO89j0: Downloading webpage
[info] Available formats for 7V_XMfO89j0:
format code  extension  resolution note
249          webm       audio only tiny   49k , webm_dash container, opus @ 49k (48000Hz), 15.11MiB
250          webm       audio only tiny   60k , webm_dash container, opus @ 60k (48000Hz), 18.57MiB
251          webm       audio only tiny  106k , webm_dash container, opus @106k (48000Hz), 32.95MiB
140          m4a        audio only tiny  129k , m4a_dash container, mp4a.40.2@129k (44100Hz), 39.88MiB
160          mp4        256x144    144p   58k , mp4_dash container, avc1.4d400c@  58k, 24fps, video only, 17.97MiB
278          webm       256x144    144p   88k , webm_dash container, vp9@  88k, 24fps, video only, 27.28MiB
133          mp4        426x240    240p  111k , mp4_dash container, avc1.4d4015@ 111k, 24fps, video only, 34.36MiB
242          webm       426x240    240p  157k , webm_dash container, vp9@ 157k, 24fps, video only, 48.39MiB
134          mp4        640x360    360p  282k , mp4_dash container, avc1.4d401e@ 282k, 24fps, video only, 86.98MiB
243          webm       640x360    360p  295k , webm_dash container, vp9@ 295k, 24fps, video only, 91.09MiB
244          webm       854x480    480p  509k , webm_dash container, vp9@ 509k, 24fps, video only, 156.93MiB
135          mp4        854x480    480p  536k , mp4_dash container, avc1.4d401e@ 536k, 24fps, video only, 165.20MiB
136          mp4        1280x720   720p  977k , mp4_dash container, avc1.4d401f@ 977k, 24fps, video only, 301.00MiB
247          webm       1280x720   720p 1008k , webm_dash container, vp9@1008k, 24fps, video only, 310.68MiB
137          mp4        1920x1080  1080p 1710k , mp4_dash container, avc1.640028@1710k, 24fps, video only, 526.94MiB
248          webm       1920x1080  1080p 1765k , webm_dash container, vp9@1765k, 24fps, video only, 543.92MiB
271          webm       2560x1440  1440p 4078k , webm_dash container, vp9@4078k, 24fps, video only, 1.23GiB
313          webm       3840x2160  2160p 10289k , webm_dash container, vp9@10289k, 24fps, video only, 3.09GiB
18           mp4        640x360    360p  511k , avc1.42001E, 24fps, mp4a.40.2 (44100Hz), 157.48MiB
22           mp4        1280x720   720p 1106k , avc1.64001F, 24fps, mp4a.40.2 (44100Hz) (best)
```

&emsp;&emsp;如果想下载4K格式的视频，那么对应的format code就是313，但是这个文件没有音轨，因此还需要下载一个音轨，例如250。

&emsp;&emsp;接下来通过命令`youtube-dl -f [format code] [url]`来下载对应清晰度的视频。

&emsp;&emsp;注意，在哪个文件夹执行命令，就会下载到哪个文件夹，所以请先切换到目标文件夹。

```
root@p1614135807:/usr/bin# youtube-dl -f 313 https://www.youtube.com/watch?v=tO0IdNNJ9Mw
[youtube] tO0IdNNJ9Mw: Downloading webpage
[download] Destination: The Legend of Mi Yue 09 Engsub (Betty Sun, Tamia Liu, Alex Fong,Huang Xuan)-tO0IdNNJ9Mw.webm
[download] 100% of 3.17GiB in 01:36
```
&emsp;&emsp;可以看出网速还是很猛的。

![youtube-dl下载速度](https://pic.lufer.cc:8089/images/2021/09/14/image77982ce962f6953c.png)

&emsp;&emsp;还可以通过 -a 的参数指定外部文件列表，这样就可以排着下载了。
![通过文件列表下载视频](https://pic.lufer.cc:8089/images/2021/09/14/imagea0a0f0fb987aeb1c.png)

# FileBrowser
&emsp;&emsp;FileBrowser是一个轻量的文件浏览器，可以对指定的文件夹进行在线的管理，官网：https://github.com/filebrowser/filebrowser

&emsp;&emsp;也是通过脚本安装
```
curl -fsSL https://raw.githubusercontent.com/filebrowser/get/master/get.sh | bash  
filebrowser -r /path/to/your/files
```

&emsp;&emsp;装好之后通过一条命令启动服务：

```
filebrowser -a 0.0.0.0 -p 9333
```
&emsp;&emsp;注意一定要通过-a参数指定address，不然默认监听127.0.0.1，是不开外网的。

&emsp;&emsp;然后就可以通过IP:3333访问了，把文件下载链接直接扔到Download Station里面，网速依然很猛。

![群辉直接从VPS下载](https://pic.lufer.cc:8089/images/2021/09/14/image.png)

# MKVtoolnix
&emsp;&emsp;下载下来的视频和音频是分开的，需要使用工具将其合成。  
&emsp;&emsp;用MKVtoolnix直接把视频和音频的webm扔进去，然后混流就可以了。

&emsp;&emsp;youtube-dl自带了FFmpeg，可以在formatcode参数中用加号连接两种格式的文件，例如本文中的：313+250，然后在下载完成后可以自动转码合成为一个文件，但是我没有测试速度，用MKVtoolnix还是挺快的。

## 赠品
附上每一集的地址
```
1 https://www.youtube.com/watch?v=yktA4VDp9VA
2 https://www.youtube.com/watch?v=kZTJTh7b4Mc
3 https://www.youtube.com/watch?v=3yOywQBiNsM
4 https://www.youtube.com/watch?v=73DUuyDf2as
5 https://www.youtube.com/watch?v=VieDD1zibZI
6 https://www.youtube.com/watch?v=_FGFUQDMlO0
7 https://www.youtube.com/watch?v=Qj3T8LyCYjM
8 https://www.youtube.com/watch?v=7V_XMfO89j0
9 https://www.youtube.com/watch?v=tO0IdNNJ9Mw
10 https://www.youtube.com/watch?v=LUUake2UarM
11 https://www.youtube.com/watch?v=O-9Nh06tNn8
12 https://www.youtube.com/watch?v=grLNjplNMVY
13 https://www.youtube.com/watch?v=7gPy3X06qHE
15 https://www.youtube.com/watch?v=v7tt-amvNh0
16 https://www.youtube.com/watch?v=a0wQdWr4Gv8
17 https://www.youtube.com/watch?v=5Yx8rvCgEyY
18 https://www.youtube.com/watch?v=PVIosau8t6o
19 https://www.youtube.com/watch?v=X4p6E__V6nY
20 https://www.youtube.com/watch?v=-2fDyopA2Zs
21 https://www.youtube.com/watch?v=KnWpO9jB_hA
22 https://www.youtube.com/watch?v=-wFJ2aIizNM
23 https://www.youtube.com/watch?v=lBpETPE0lRk
24 https://www.youtube.com/watch?v=TFOUjobZ2-U
25 https://www.youtube.com/watch?v=b2uOQc6O5k4
26 https://www.youtube.com/watch?v=mSJnFRhd1vI
27 https://www.youtube.com/watch?v=Sf5D4K1eOj8
28 https://www.youtube.com/watch?v=P9RE-qAnaHg
29 https://www.youtube.com/watch?v=0XNw1Crdip0
30 https://www.youtube.com/watch?v=U6FBxMnnk9U
31 https://www.youtube.com/watch?v=alaF0ztP6kc
32 https://www.youtube.com/watch?v=VMA8Pr678Yw
33 https://www.youtube.com/watch?v=cYNHfWAN41o
34 https://www.youtube.com/watch?v=i2hF2RGKWTI
35 https://www.youtube.com/watch?v=YPNzNcG-4UE
36 https://www.youtube.com/watch?v=28T_bQLOm2k
37 https://www.youtube.com/watch?v=_2yYyqBFfxU
38 https://www.youtube.com/watch?v=aEGRwZXH5hE
39 https://www.youtube.com/watch?v=apQRXmV8EoY
40 https://www.youtube.com/watch?v=QsZynSHNzGI
41 https://www.youtube.com/watch?v=Z05B40t2y-U
42 https://www.youtube.com/watch?v=Svp5V_Cdq8k
43 https://www.youtube.com/watch?v=Sj2QHoZI-7U
44 https://www.youtube.com/watch?v=qrN_QSZFbSw
45 https://www.youtube.com/watch?v=FCR4DfzQU3s
46 https://www.youtube.com/watch?v=xL8cVQsGaIM
47 https://www.youtube.com/watch?v=oSqRdkBS1a4
48 https://www.youtube.com/watch?v=lEmq1A-IkaM
49 https://www.youtube.com/watch?v=3e5Fl6UIhtA
50 https://www.youtube.com/watch?v=SejoHQ1eJ-o
51 https://www.youtube.com/watch?v=drjcavhM4gg
52 https://www.youtube.com/watch?v=x59BV7MEMnw
53 https://www.youtube.com/watch?v=aVypQle_jVs
54 https://www.youtube.com/watch?v=X33RHPR8RNg
55 https://www.youtube.com/watch?v=yIE-gHuLYt8
56 https://www.youtube.com/watch?v=jqIAwXMk_nI
57 https://www.youtube.com/watch?v=DYbhwDhfnmY
58 https://www.youtube.com/watch?v=tN_lyKYBh8Y
59 https://www.youtube.com/watch?v=OFwIYumZyCE
60 https://www.youtube.com/watch?v=S4eImHQj-NE
61 https://www.youtube.com/watch?v=6uAchtInjRk
62 https://www.youtube.com/watch?v=oXkwjc92EGM
63 https://www.youtube.com/watch?v=Z1DjUozztsk
64 https://www.youtube.com/watch?v=7GLWjMVyYX0
65 https://www.youtube.com/watch?v=s54_4brwAgo
66 https://www.youtube.com/watch?v=G0VHCJ-P9bA
67 https://www.youtube.com/watch?v=9R6GfKoHMSo
68 https://www.youtube.com/watch?v=V1aCulCCtZk
69 https://www.youtube.com/watch?v=UNdGdgaHumg
70 https://www.youtube.com/watch?v=bmkgt5EPj30
71 https://www.youtube.com/watch?v=PWYGZfODhWQ
72 https://www.youtube.com/watch?v=xfhL4WPMXvE
73 https://www.youtube.com/watch?v=7cQIMqOivWg
74 https://www.youtube.com/watch?v=DPveNEoUh5A
75 https://www.youtube.com/watch?v=c4sYs8lhLRA
76 https://www.youtube.com/watch?v=mNhoOJnhsLs
77 https://www.youtube.com/watch?v=IzFIlVhMFg0
78 https://www.youtube.com/watch?v=Lf5_NitFcyI
79 https://www.youtube.com/watch?v=D6aVR0ah3Lg
80 https://www.youtube.com/watch?v=mAz1NBTBgzQ
81 https://www.youtube.com/watch?v=Zm_XHSSeXis
```
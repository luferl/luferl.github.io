---
title: Hexo+GitHub搭建博客(三) 文章的撰写与发布
date: 2018-05-17 22:50:36
categories: Hexo
tags: [Github,Hexo]
---

* [开始前的准备](#开始前的准备)
* [建立第一篇文章](#建立第一篇文章)
* [文章解析与Markdown语法简要介绍](#文件解析与Markdown语法简要介绍)
* [文章发布](#文章发布)


## 开始前的准备

&emsp;&emsp;文章怎么能没有图呢，所以为了配图，我们要先修改Test文件夹下的_config.yml,把“post_asset_folder“设置为true”，这样就会自动识别图片。

&emsp;&emsp;可以装个Visual Studio Code，因为它支持Markdown的自动渲染，就可以看见目标页面长啥样啦，就像下图一样。

![](https://pic.lufer.cc:8089/images/2021/03/15/e4xbQ0.png)

## 建立第一篇文章

&emsp;&emsp;在项目文件夹下，输入
```bash
hexo new post "First Post"
```
&emsp;&emsp;或者直接在source\\_posts\目录下新建First Post.md和一个名为First Post的文件夹。

&emsp;&emsp;然后我们编辑这个.md文件就可以啦。

## 文章解析与Markdown语法简要介绍

&emsp;&emsp;每个通过`hexo new post`创建的md文件都包含以下文件头，如果是自己创建的md文件，则要把这个头部加进去，所以我建议直接复制以前的md改个名字就好啦，但是记得要改时间哦。

```
---
title: Hexo+GitHub搭建博客(三) 文章的撰写与发布
date: 2018-05-17 21:17:36
category: Github
tags: [Github,Hexo]
---

```
&emsp;&emsp;title是文章标题，在这里写过了之后下面的正文就不要写啦。  
&emsp;&emsp;date 是写这篇文章的日期，将来hexo是要按照这个排序的。  
&emsp;&emsp;category 是你希望这篇文章所属的分类目录。  
&emsp;&emsp;tags 是你给这篇文章添加的标签，如果只有一个标签就直接打就好啦，如果想要多个标签则打成如下形式`[标签1,标签2,标签3]`。

&emsp;&emsp;然后就可以写正文啦！

### 标题
```
# 一级标题
## 二级标题
### 三级标题
```

&emsp;&emsp;Markdown用#来控制标题，如果需要一级标题，就打一个#然后打一个空格，然后打上标题就可以了,像下面这样。
```
# 一级标题
```

&emsp;&emsp;二级标题就打两个#，三级就打三个。

>如果想打出来这种效果呢，就在这行最前面打一个>就可以了

### 换行
&emsp;&emsp;有三种方式：
1. 打两个空格
2. 在需要换行的地方打一个\<br\>  
3. 打两个回车，但是这样中间会空一个小行

### 插入图片
&emsp;&emsp;把图片放到同名的文件夹里，在需要插入的地方输入`{% asset_img imagename.png %}`。

&emsp;&emsp;如果需要特殊字体与颜色。
```
*斜体文本*    _斜体文本_
**粗体文本**    __粗体文本__
***粗斜体文本***    ___粗斜体文本___

<font color=green>INFO</font>  这样就会有一个绿色的INFO

```

### 添加链接
```
常用链接方法
文字链接 [链接名称](https://chwshuang.github.io)
网址链接 <https://chwshuang.github.io>
```
### 制作列表
```
普通无序列表

- 列表文本前使用 [减号+空格]
+ 列表文本前使用 [加号+空格]
* 列表文本前使用 [星号+空格]

普通有序列表

1. 列表前使用 [数字+空格]
2. 我们会自动帮你添加数字
7. 不用担心数字不对，显示的时候我们会自动把这行的 7 纠正为 3

列表嵌套

1. 列出所有元素：
    - 无序列表元素 A
        1. 元素 A 的有序子列表
    - 前面加四个空格
2. 列表里的多段换行：
    前面必须加四个空格，
    这样换行，整体的格式不会乱
3. 列表里引用：

    > 前面空一行
    > 仍然需要在 >  前面加四个空格


```


## 文章发布

&emsp;&emsp;文章写完了？发布只需要一行：

>CD test  
>hexo d -g
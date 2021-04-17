---
title: 按目录存储Hexo文章并修改生成的链接
date: 2021-04-06 11:59:30
categories: Hexo
tags: [Github,Hexo]
---
&emsp;&emsp;随着Hexo文章逐渐变多，都放在source文件夹下的话想找某篇文章进行管理就显得有些痛苦了，所以这次我打算建立一些文件夹按照不同类别来管理文章。

&emsp;&emsp;只需要在`_posts`下面建立对应的文件夹然后把md文件放进去就可以了。

&emsp;&emsp;但是这样生成的页面地址会是`域名/年/月/日/目录/文章名`。这种链接太长了，而且我也不喜欢按照年月日来生成链接。

&emsp;&emsp;修改`_config.yml`中的`permalink`。

&emsp;&emsp;`permalink`设定的是生成的链接的格式，默认如下：
```yml
permalink: :year/:month/:day/:title/
```
&emsp;&emsp;也就是按照`/年/月/日/文章名`的方式来生成，而文章名在我们设置了文件夹后将会包含/目录/文章名。删掉年月日即可只用目录来管理链接。

```yml
permalink: :title/
```

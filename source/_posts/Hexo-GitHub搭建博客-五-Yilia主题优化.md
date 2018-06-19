---
title: Hexo+GitHub搭建博客(五) Yilia主题优化
date: 2018-05-18 14:44:14
tags: [Github,Hexo]
categories: Code
---

Yilia主题还是挺漂亮的，但是还是有一些小BUG或者需要改进的地方。

## 分类目录双斜线问题

当你点击一个分类目录时，URL会变成 YourSite/Categories/Category//

结尾多了一个斜线。

解决方案：

修改yilia\layout\\_partial\post\category.ejs第7行
```
<a href="<%= config.root %><%= tag.path %>/" class="article-tag-list-link color<%= tag.name.length % 5 + 1 %>"><%-tag.name%></a>  
```
删掉/
```
<a href="<%= config.root %><%= tag.path %>" class="article-tag-list-link color<%= tag.name.length % 5 + 1 %>"><%-tag.name%></a>
```

## 头像保存位置问题

头像保存到theme\yilia\sorce\img下，假设为headimg.jpg

然后在主题的_config.yml下修改“avatar: img/headimg.jpg”

这里有一个BUG，就是在这里的头像仅能在首页显示，如果需要在所有页面均可显示，则需要进行修改

PC端修改 theme\yilia\layout\\_partial\left-col.ejs
```
<a href="<%=theme.root%>" class="profilepic">
	<img src="<%=theme.avatar%>" class="js-avatar">
</a>
```
修改为

```
<a href="<%=theme.root%>" class="profilepic">
	<img src="<%=theme.root+theme.avatar%>" class="js-avatar">
</a>
```
主要修改img那行的src位置。

移动端头像需要修改theme\yilia\layout\\_partial\mobile-nav.ejs，9-11行
```
			<div class="profilepic">
				<img src="<%=theme.avatar%>" class="js-avatar">
			</div>
```
修改为

```
			<div class="profilepic">
				<img src="<%=theme.root+theme.avatar%>" class="js-avatar">
			</div>
```


## 目录页与标签页的建立

这个主题是不带目录页和标签页的，需要我们自己实现。

首先修改yilia\layout\page.ejs,把对于categories与tags的判断加上，并分别指向categories-page与tags-page两个模板。

```
<% if ('categories' == page.type) { %>
    <%- partial('_partial/categories-page', {post: page, index: false}) %>
  <% } else if ('tags' == page.type) { %>
    <%- partial('_partial/tags-page', {post: page, index: false}) %>
  <% } else { %>
    <%- partial('_partial/article', {post: page, index: false}) %>
  <% } %>
```

随后我们建立categories-page模板页，在_partial下新建categories-page.ejs

```
<section class="archives-wrap">
  <div class="archive-year-wrap">
    <a href="#" class="archive-year">全部分类</a>
  </div>
  <div class="archives">
    <article class="archive-article archive-type-category">
      <div class="archive-article-inner">
        <header class="archive-article-header">
          <div class="article-info">
            <div class="article-category tagcloud">
              <ul class="article-tag-list">
                <% site.categories.each(function(tag, i) { %> 
                  <li class="article-tag-list-item">
                    <a href="<%= config.root %><%= tag.path %>/" class="article-tag-list-link color<%= tag.name.length % 5 + 1 %>"><%- tag.name %></a>
                  </li>
                <% }) %>
              </ul>
            </div>
          </div>
        </header>
      </div>
    </article>
  </div>
</section>
<% site.categories.each(function (category) { %>
  <section class="archives-wrap">
    <div class="archive-year-wrap">
      <a href="<%- url_for(category.path) %>" class="archive-year"><%= category.name %></a>
    </div>
    <div class="archives">
      <% var i = 0 %>
      <% site.posts.each(function (post) { %>
        <% var belong = false; %>
        <% post.categories.each(function (c) { %>
          <% if (c.name == category.name) { %>
            <% belong = true; %>
          <% } %>
        <% }) %>
        <% if (belong) { %>
          <% i = i+1 %>
          <%- partial('_partial/archive-post', {post: post, even: i % 2 == 0, index: true}) %>
        <% } %>
      <% }) %>
    </div>
  </section>
<% }) %>
```

同理建立tags-page.ejs
```
<section class="archives-wrap">
	<div class="archive-year-wrap">
	  <a href="#" class="archive-year">全部标签</a>
	</div>
	<div class="archives">
	  <article class="archive-article archive-type-category">
		<div class="archive-article-inner">
		  <header class="archive-article-header">
			<div class="article-info">
			  <div class="article-category tagcloud">
				<ul class="article-tag-list">
				  <% site.tags.each(function(tag, i) { %> 
					<li class="article-tag-list-item">
					  <a href="<%= config.root %><%= tag.path %>/" class="article-tag-list-link color<%= tag.name.length % 5 + 1 %>"><%- tag.name %></a>
					</li>
				  <% }) %>
				</ul>
			  </div>
			</div>
		  </header>
		</div>
	  </article>
	</div>
  </section>
  <% site.tags.each(function (tag) { %>
	<section class="archives-wrap">
	  <div class="archive-year-wrap">
		<a href="<%- url_for(tag.path) %>" class="archive-year"><%= tag.name %></a>
	  </div>
	  <div class="archives">
		<% var i = 0 %>
		<% site.posts.each(function (post) { %>
		  <% var belong = false; %>
		  <% post.tags.each(function (c) { %>
			<% if (c.name == tag.name) { %>
			  <% belong = true; %>
			<% } %>
		  <% }) %>
		  <% if (belong) { %>
			<% i = i+1 %>
			<%- partial('_partial/archive-post', {post: post, even: i % 2 == 0, index: true}) %>
		  <% } %>
		<% }) %>
	  </div>
	</section>
  <% }) %>
```
新建categories和tags页面

>hexo new page categories  
>hexo new page tags

修改page head

```
index.md:

---
title: 分类
date: 2018-05-18 00:50:24
type: "categories"
---
```
同理修改tags不细说。

修改yilia\_config.yml,Menu中加上两个页面。
```
分类: /categories
标签: /tags
```

至此完成两个页面的建立。

不过对于标签页，有自建的smart-menu，支持标签云的检索。

对于目录页，已经有很多Issue，作者表示将来会加上，只是还没想好做成什么样子而已。
---
title: Github-page 增加分类
category: github-page
---

  因为想到博客还没有分类功能，于是就搜 `jekyll` 的分类方法，用到了 `jekyll` 的 `category` 特性， 顺利给博客加上了分类功能。

下面是博客的分类功能

![category_1](http://qcdn.hjsite.cn/image/blog/categeory/category_1.png)

  前面部分指分类的名称，括号内的指该分类下的文章数

  下面是分类下的文章列表

![category_2](http://qcdn.hjsite.cn/image/blog/categeory/category_2.png)

  方法：

##### 1. 在所有文章上添加 `category` 标签

  将 `{分类名}` 替换

```
---
layout: post
title: 标题
category: {分类名}
---
```


##### 2. 在根目录新建 `category_index.html` 文件，并加入下面代码

  遍历所有分类，显示分类列表，指向的是 `/category/{分类名}.html`

  注意：将 `\` 去除（我的页面会进行编译）

```html
---
  title: 文章分类
  layout: page
---
<ul 
{\% for category in site.categories %\}
<li 
  <a href="/category/{\{ category | first }\}/" {\{ category | first }\} </a 
  <span ({\{ category | last | size }\})</span 
</li 
{\% endfor %\}
</ul 
```

  在我的模板上，创建完后就会出现在左侧导航上

##### 3. 建立对应的分类文件

  创建 `category` 目录 ，在目录下建 `/category/{分类名}.html`

  文件将显示所有对应分类名下的文章

  注意：将 `\` 去除（我的页面会进行编译）

```html
  ---
  title: Ubuntu
  layout: category
  ---
  <ul 
  {\% for post in site.categories.{分类名} %\}
  <li 
    <span <small {\{ post.date | date_to_string }\}</small </span 
    <a href='{\{ site.baseurl }\}{{ post.url }}'  {\{ post.title }\}</a 
  </li {\% endfor %\}
  </ul 
```

##### 4. 查看自己的分类功能

![category_3](http://qcdn.hjsite.cn/image/blog/categeory/category_3.png)

  可能会因为对应该目录的不同而显示 `404`，就需要按照自己的环境来替换其中的参数，如 `/category/\{\{ category | first \}\}/`

  至此，`jekyll category` 的分类功能就添加好了。

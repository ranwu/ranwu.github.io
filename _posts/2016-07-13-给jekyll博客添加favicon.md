---
layout: post
title:  "给jekyll博客添加favicon"
date:   2016-07-13 22:12:33 +0800
categories: jekyll tutor
---

## 1. 下载favicon
到[IconArchive](http://www.iconarchive.com/)搜索喜欢的图标。一般来说，在网页左侧的`Size`中选择`32px*32px`，然后在网页顶部的搜索栏中输入关键字进行搜索。比如，我选择了32的Size，并且在搜索栏中输入关键字`emoji`，然后就显示出如下所示的结果：
![searchResult](/photo/searchResult.png)

然后将鼠标移动到图标上去，点击`PNG`格式即开始下载图标。

## 2. 制作favicon
使用在线制作工具[Favicon-generator](http://www.favicon-generator.org/)来制作favicon。此工具的好处是可以生成各种平台的图标，几乎是一次生成，全平台使用。

**点击上传按钮，上传图片，并确认**

>注意，上传的图片不能是`.ico`格式的图片。

## 3. 下载图片并应用到网站
在制作完成后，如果成功的话会跳转到图片下载页面，并且下面还有一段`HTML`代码。如下图所示：
![downloadPage](/photo/downloadPage.png)

然后把图片拷贝到网站图片目录，我是放到了`/img`目录。

然后将代码嵌入到模板文件`/_layouts/default.html`的`<head>`标签中:
{% highlight html %}
<html>
  <head>
    <link rel="apple-touch-icon" sizes="57x57" href="/img/apple-icon-57x57.png">
    <link rel="apple-touch-icon" sizes="60x60" href="/img/apple-icon-60x60.png">
    <link rel="apple-touch-icon" sizes="72x72" href="/img/apple-icon-72x72.png">
    <link rel="apple-touch-icon" sizes="76x76" href="/img/apple-icon-76x76.png">
    <link rel="apple-touch-icon" sizes="114x114" href="/img/apple-icon-114x114.png">
    <link rel="apple-touch-icon" sizes="120x120" href="/img/apple-icon-120x120.png">
    <link rel="apple-touch-icon" sizes="144x144" href="/img/apple-icon-144x144.png">
    <link rel="apple-touch-icon" sizes="152x152" href="/img/apple-icon-152x152.png">
    <link rel="apple-touch-icon" sizes="180x180" href="/img/apple-icon-180x180.png">
    <link rel="icon" type="image/png" sizes="192x192"  href="/img/android-icon-192x192.png">
    <link rel="icon" type="image/png" sizes="32x32" href="/img/favicon-32x32.png">
    <link rel="icon" type="image/png" sizes="96x96" href="/img/favicon-96x96.png">
    <link rel="icon" type="image/png" sizes="16x16" href="/img/favicon-16x16.png">
    <link rel="manifest" href="/img/manifest.json">
    <meta name="msapplication-TileColor" content="#ffffff">
    <meta name="msapplication-TileImage" content="/ms-icon-144x144.png">
    <meta name="theme-color" content="#ffffff">
  </head>
{% endhighlight %}


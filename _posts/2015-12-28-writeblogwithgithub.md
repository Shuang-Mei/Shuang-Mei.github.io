---
layout: post
title: "如何使用GitHub进行代码（文件）分享和blog书写"   
description: "GitHub是程序员中的facebook，可以在GitHub上面进行代码管理、共享、协同开发等诸多管理的功能。除此之外，GitHub的blog page功能也是诸多技术blog的平台。对我这个小白，需要从头到尾整理并记录下如何使用GitHub的操作步骤。"
category: 'project experience'
---

#如何使用GitHub进行代码（文件）分享和blog书写

  GitHub是程序员中的facebook，可以在GitHub上面进行代码管理、共享、协同开发等诸多管理的功能。除此之外，GitHub的blog page功能也是诸多技术blog的平台。对我这个小白，需要从头到尾整理并记录下如何使用GitHub的操作步骤。
##一. GitHub的文件分享步骤
###1. 准备工作
&#160; &#160; &#160; &#160;包括申请GitHub账号，安装Git软件等

###2. 配置Git
  &#160; &#160; &#160; &#160;也就是将你的账号和你的git软件对应，第一次使用时候需要配置，具体的配置见[http://my.oschina.net/bxxfighting/blog/378196?fromerr=lDM5eBuw](http://my.oschina.net/bxxfighting/blog/378196?fromerr=lDM5eBuw)

&#160; &#160; &#160; &#160;第二次使用的时候，不需要配置，但是需要测试是否连接成功。测试代码
`ssh –T git@github.com`。成功则可以进行下一步操作

###3. 创建一个Repository
A)在GitHub上创建一个Repository叫做testRepository。

B)本地化Repository的创建连接步骤：

新建一个文件夹；

在这个文件夹上打开Git终端；

输入`git init`；

远程添加一个库 `git remote add origin git@github.com:yong-lee2015/testRepository`。（存在同名库则报错）；

这一步应该算是提交了，代码。 ` git pull git@github.com:yong-lee2015/testRepository`。

在文件夹中 做你自己的（比如：新建一个txt文档）

**添加文档。`git add .`**

**添加评论。`git commit –m “这里写下你自己的记录本次提交内容的信息”`**

**发布。`git push git@github.com:yong-lee2015/testRepository`**

&#160; &#160; &#160; &#160;现在就基本上可以使用了，每次增加了新文件就先add，然后commit，如果只是改了文件的内容，只执行commit就行了，当然最后一步都是要执行push，把所以改变推送到我们的github上去托管。现在就基本上可以使用了，每次增加了新文件就先add，然后commit，如果只是改了文件的内容，只执行commit就行了，当然最后一步都是要执行push，把所以改变推送到我们的github上去托管。

##二. GitHub中blog的书写

&#160; &#160;&#160;&#160; MarkDownPad(用于写blog，这篇文章就是MD写的)；GitHub DeskTop（方便管理文件）；
    
###1. 安装Jekyll
主要参考网页[http://blog.fens.me/jekyll-bootstarp-github/](http://blog.fens.me/jekyll-bootstarp-github/)来下载安装Ruby、安装GEM，安装Jekyll

a) 安装Ruby 没有什么困难。查看version 的代码：`ruby -v`

b）安装Gem。由于gem的官网不是很稳，常常使用[https://ruby.taobao.org/](https://ruby.taobao.org/)。查看ruby包的代码：`gem list`

c）安装Jekyll。直接使用`gem install jekyll`就可以了。然后使用命令`jekyll`检测是否安装成功

###2. Jekyll构建基于bootstrap模板

a）从github网上down一个网页模板

b）ruby 到这这个目录（注意 cd 和直接F：的用法）

c）中间有很多步骤略去

###3. 网址的发布
在这里，我是借鉴阮一峰的网址[http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)

a)`$ ssh -T git@github.com;$ git init;$ git remote set-url origin git@github.com:yong-lee2015/jekyll-demo.git;$ git branch gh-pages;$ git add .; git checkout --orphan gh-pages;$ git add .;$ git commit -m "first post";$ git remote add origin https://github.com/yong-lee2015/jekyll-demo.git;$ git push origin gh-pages`

反正经过一系列的命令，blog就可以发表了



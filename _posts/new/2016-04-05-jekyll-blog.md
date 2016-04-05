---
layout: post
title: 如何搭建一个 Jekyll 博客
category: 技术
tags: jekyll
description: 搭建一个 Jekyll 博客
---

## 1.Jekyll 简介
>Jekyll 是一个简单的博客形态的静态站点生产机器。它有一个模版目录，其中包含原始文本格式的文档，通过 [Markdown](http://daringfireball.net/projects/markdown/) （或者 [Textile](http://textile.sitemonks.com/)） 以及 [Liquid](http://docs.shopify.com/themes/liquid-basics) 转化成一个完整的可发布的静态网站。


新开的这个博客就是基于**[Jekyll](http://jekyll.bootcss.com/ "http://jekyll.bootcss.com/")**，代码托管在[Coding](https://coding.net/u/parallel/p/hanchan/git)，使用了Coding的演示([http://docs.coding.io/](http://docs.coding.io/)),为啥不用[GitHub Page](https://pages.github.com/),主要是在国内访问github感觉卡，GitHub Page的环境Coding也提供了，体验要好很多，以后再考虑上GitHub。

## 2.Jekyll 安装
jekyll是用ruby写的，确保你的系统内已安装 [Ruby](https://www.ruby-lang.org)，我的开发环境已经具备了ruby，使用ruby2.3

	rvm use 2.3.0

安装 Jekyll 的最好方式就是使用RubyGems,所有的 Jekyll 的 gem 依赖包都会被自动安装：

{% highlight sh %}
```bash
$ gem install jekyll
```
{% endhighlight %}

检查安装下面相关的gem包：

{% highlight sh %}
```bash
$ gem install kramdown // markdown语言解析包
$ gem install pygments.rb // 代码高亮包
$ gem install liquid 
```
{% endhighlight %}

注意：高亮包需要python2.7的环境

## 3.Jekyll 使用

### 3.1 使用默认模板：

```bash
jekyll new my
```

- _layouts：存放模板
- _includes:存放HTML代码段
- _posts：存放博客文章
- _coinfig.yml：配置文件

接着在项目内执行下面的命令启动本地服务器：

```bash
jekyll serve
```
更复杂的用法请参考 [jekyll 教程](http://jekyllcn.com/docs/home/)

效果如下：

![jekyll-new-site](http://7xr422.com1.z0.glb.clouddn.com/jekyll-new-1.png)

可以看到，界面还是比较简洁大方的。

### 3.2 使用fork的模板：

套用别人的分享模板，这样可以很快的建起博客，开始写文章。
之后可以在别人的模板基础上，形成自己的风格。

本博客套用了[3-Jekyll Theme](https://github.com/P233/3-Jekyll)

至此，本地的jekyll环境搭建完毕，写完文章后，先在本地看效果，待确认没问题了，推送到git远程仓库

## 4.自动部署（coding）

### push 自动部署的方法

1.点击**演示**，**环境变量**，设置 WEBHOOK_TOKEN 变量为**任意值**

![jekyll-push-env](http://7xr422.com1.z0.glb.clouddn.com/jekyll-push-env.png)

2.点击设置，webhook，设置 url 为 "应用地址/\_"，token 设为第2步的 WEBHOOK_TOKEN 值

![jekyll-push-webhook](http://7xr422.com1.z0.glb.clouddn.com/jekyll-push-webhook.png)

3.重启应用

这样，在我们将文章推送到Coding仓库时候，会自动部署到演示环境









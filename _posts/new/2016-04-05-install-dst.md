---
layout: post
title: 使用Vagrant构建Data Science环境
category: 技术
tags: vagrant,data-science，tools
description: 安装data-science-toolbox
---
## 1.关于DST
DST是[data-science-toolbox](https://github.com/jeroenjanssens/data-science-at-the-command-line "data-science-at-the-command-line")，基于vagrant构建，里面集成了很多命令行工具，包括[csvkit](http://csvkit.readthedocs.org/en/0.9.1/ "csvkit")、[jq](https://stedolan.github.io/jq/manual/ "jq")、Rio等处理csv和json的命令行神器，也配置好了python、R等环境。


## 2.安装
参考：[http://datascienceatthecommandline.com/](http://datascienceatthecommandline.com/ "dst")

### Step 1:VirualBox
 - 下载VirtualBox([https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads "virtualbox")) 
 - 安装


### Step 2:Vagrant

 - 下载Vagrant（[https://www.vagrantup.com/downloads.html](https://www.vagrantup.com/downloads.html "Vagrant")）
 - 安装（[https://www.vagrantup.com/docs/installation/](https://www.vagrantup.com/docs/installation/ "installation")）

### Step 3:DST
新建工作目录，并执行初始化工作：

{% highlight bash %}
```bash
$ mkdir dst
$ cd dst
vagrant init data-science-toolbox/data-science-at-the-command-line
```
{% endhighlight %}

会生成Vagrantfile文件，内容如下：
	
	# Every Vagrant development environment requires a box. You can search for
 	# boxes at https://atlas.hashicorp.com/search.	
	Vagrant.configure(2) do |config|
	  config.vm.box = "data-science-toolbox/data-science-at-the-command-line"
	end

然后执行

	vagrant up

输出如下：

{% highlight bash %}
```bash
$ vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Box 'data-science-toolbox/data-science-at-the-command-line' could not be found. Attempting to find and install...
    default: Box Provider: virtualbox
    default: Box Version: >= 0
==> default: Loading metadata for box 'data-science-toolbox/data-science-at-the-command-line'
    default: URL: https://atlas.hashicorp.com/data-science-toolbox/data-science-at-the-command-line
==> default: Adding box 'data-science-toolbox/data-science-at-the-command-line' (v1.0.0) for provider: virtualbox
    default: Downloading: https://atlas.hashicorp.com/data-science-toolbox/boxes/data-science-at-the-command-line/versions/1.0.0/providers/virtualbox.box
==> default: Box download is resuming from prior download progress
    default: Progress: 0% (Rate: 80076/s, Estimated time remaining: 4:27:57)
```
{% endhighlight %}

因为第一次启动过程会去下载data science对应的box文件，国内下载这个东西不稳定，我们通过其他下载工具把这个[dst.box](https://atlas.hashicorp.com/data-science-toolbox/boxes/data-science-at-the-command-line/versions/1.0.0/providers/virtualbox.box "dst")下载下来。

我已经上传到网盘，[戳这里](http://pan.baidu.com/s/1ge3n3LT "dst-1.0.box")下载

将下载的dst-dsatcl-1.0.0.box放在之前新建的工作目录里，执行：

	$vagrant box add --force data-science-toolbox/data-science-at-the-command-line path:\dst\dst-dsatcl-1.0.0.box

手动添加box文件，再次使用vagrant up启动，OK。

### Step 4:login

在vagrant up时候输出了很多信息，其中有几行：
	
	...
	default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
	...

- 使用shell终端，连接127.0.0.1:2222,登陆名为vagrant
- 密钥:.vagrant\machines\default\virtualbox\private_key

![login-dst](http://7xr422.com1.z0.glb.clouddn.com/login-dst.png)












































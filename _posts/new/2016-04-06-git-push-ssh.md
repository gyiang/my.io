---

layout: post
title: git使用ssh免登录及原理
category: 技术
tags: ssh,git
description: 介绍git的ssh免登录方式及原理

---

## 1.背景
使用git push时候，要输入账号密码进行权限验证，push多了还是感觉很麻烦的，影响效率，于是用ssh key方式push，并且SSH传输的数据是经过压缩的，可以加快传输，在安全上，可以防止[中间人攻击](https://zh.wikipedia.org/wiki/%E4%B8%AD%E9%97%B4%E4%BA%BA%E6%94%BB%E5%87%BB)。

## 2.SSH 免登录原理

>SSH是[Secure Shell](https://zh.wikipedia.org/wiki/Secure_Shell)，SSH为一项创建在应用层和传输层基础上的安全协议，为计算机上的Shell（壳层）提供安全的传输和使用环境。

在客户端来看，SSH提供两种级别的安全验证。

- 第一级别：基于密码的安全验证，当通过帐号和密码登录远程主机后，所传输的数据都会被加密，因为可能会有别的服务器在冒充真正的服务器，无法避免被“中间人”攻击。
- 第二级别：**基于密钥的安全验证**，依靠密钥，也就是你必须为自己创建一对密钥（**公有密钥：id_rsa.pub**、**私有密钥：id_rsa**），并把公有密钥放在需要访问的服务器上。客户端软件会向服务器发出请求，请求用你的密钥进行安全验证。服务器收到请求之后，先在你在该服务器的用户根目录下寻找你的公有密钥，然后把它和你发送过来的公有密钥进行比较。如果两个密钥一致，服务器就用公有密钥加密“质询”（challenge）并把它发送给客户端软件。从而避免被“中间人”攻击。

基于密钥的安全验证也是ssh免登录的基础，具体原理看下图：

![](http://7xr422.com1.z0.glb.clouddn.com/ssh-sign-working.png)

这样是不是就很清晰啦。
当我们把id_rsa.pub共有密钥放在需要访问的服务器（Github、Coding等）后，就建立了本地、远程验证关系，通过git push推送分支到远程仓库时候，相当于向服务器发送请求时，服务器会进行ssh验证，验证通过后就免去了输入密码。

## 3.SSH for git

首先：

	ssh-keygen -t rsa -C "your_email@outlook.com"

windows下可以在git bash(mingw环境）下执行，-t 表示加密类型，用rsa，-C comment

**注意**，在生成密钥的时候不要对SSH私钥加密（直接2次回车让密钥密码为空即可），否则仍然需要使用密码来访问。

本来想写下具体怎么配置时候，发现Coding的帮助文档已经说的很清楚了。[戳这里](https://coding.net/help/doc/git/ssh-key.html)

> 账户 SSH 公钥是跟用户账户关联的公钥，一旦设置，就拥有账户下所有项目仓库的读写权限。

>本地打开id_rsa.pub文件，复制其中全部内容，填写到[SSH_RSA公钥key](https://coding.net/user/account/setting/keys)下的一栏，公钥名称可以随意起名字。
完成后点击“添加”，然后输入密码或动态码即可添加完成。

![coding-ssh-config](http://7xr422.com1.z0.glb.clouddn.com/coding-ssh-config.png)

配置后，在本地提交时候可以直接git push（配置了SSH公钥后，需要使用SSH地址操作仓库），不用再输入平台账号密码。

	git remote remove origin
	git remote add origin git@git.coding.net:user/repo.git
    git push -u origin master

>遇到询问是否信任服务器公钥，输入 yes 即可











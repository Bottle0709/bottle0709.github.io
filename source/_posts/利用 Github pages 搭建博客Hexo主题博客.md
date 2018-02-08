---
title: 利用 Github pages 搭建博客Hexo主题博客
date: 2018-01-6 11:47:40
update: 2018-01-10 16:47:34
top: 60
tags:
- github
- hexo
categories: Hexo
password: 
cover_picture: http://p3nn031ge.bkt.clouddn.com/blog/180206/jhF88k5IE7.png?imageslim
---

![mark](http://p3nn031ge.bkt.clouddn.com/blog/180206/jhF88k5IE7.png?imageslim)

## 1.前言
&emsp;一直想搭建一个自己的个人博客，看了很多种搭建的方法，最后选择了github pages服务搭建，主要看中以下好处：

 * 全是静态文件，访问速度快；
 
 * 数据绝对安全，基于github的版本管理；
 
 * 免费方便，不用花一分钱就可以搭建（毕竟还是一名学生党，目前还没有资金购买服务器）。
 
&emsp;而使用github pages搭建博客有两种方式，hexo和jekyll，当时我先采用的是jekyll方式搭建，但由于配置环境时一直出现错误，查了很多资料无法解决，就转战到hexo方式搭建。在此过程中，折腾博客的各种配置以及功能占具了我一部分时间，现通过文章记录过程，以免过后遗忘，且当备份之用。

## 2.准备工作
&emsp;在开始之前，你必须已经

 * 有一个github账号，没有的话先去注册一个；
 
 * 安装node.js、npm，并了解相关基础知识； 
 
 * 安装git for windows(或者其他git客户端) 。
 
&emsp;上面几点操作的具体步骤，找度娘即可，我就不一一称述了。

## 3.搭建github博客
### &emsp;3.1.**创建仓库**

----------

&emsp;进入github官网登录你的账号，新建一个名为`你的用户名.github.io`的仓库。
&emsp;例如：，你的github用户名是zhangsan，那么你新建`zhangsan.github.io`的仓库（必须是你的用户名，其他名称无效），将来你的网站访问地址就是http://zhangsan.github.io，这样是不是很方便？
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/JKKL2eD8H0.png?imageslim)

&emsp;需要注意的几个地方：

 * 注册的邮箱一定要验证，否则不会成功；
 
 * 仓库名字必须是：`username.github.io`,其中`username`是你的用户名；
 
 * `Initialize this repository with a READEM`选项一定要勾选。
### &emsp;3.2.**配置SSH Key**

----------

&emsp;为什么要配置这个呢？因为你提交代码肯定要拥有的github权限才可以，但直接使用用户名和密码不太安全，所以我们用SSH Key来解决本地和服务器的连接问题。


&emsp;1.打开 Git Bash ,设置 Git 的user name 和 email(如果是第一次的话)，这里的用户名和邮箱替换成你自己的。
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/2i59EgGHH9.png?imageslim)

&emsp;2.输入`cd ~/.ssh`,检查是否有.ssh的文件。
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/C7C085geGH.png?imageslim)

&emsp;3.输入`ls`,列出该文件下的内容，说明存在.ssh文件。
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/fCegJA2I1l.png?imageslim)

&emsp;4.如果不显示，则输入`ssh-keygen -t rsa -C “你的邮箱”`，连续三个回车，生成密钥，最后得到了两个文件：id_rsa和id_rsa.pub（默认存储路径是：C:\Users\Administrator\.ssh）。
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/4i0c1hclJb.png?imageslim)

&emsp;5.打开用户目录，找到.ssh\id_rsa.pub文件，记事本打开并复制里面的内容，打开你的github主页，进入个人设置 -> SSH and GPG keys -> New SSH key ,将刚复制的内容粘贴到key那里，title写项目的名字，保存。
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/GKmBFbmhja.png?imageslim)

&emsp;6.输入`ssh -T git@github.com`（注意邮箱地址不用改），测试添加ssh是否成功。如果看到Hi后面是你的用户名，就说明成功了。
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/K13CDbffJh.png?imageslim)
### &emsp;3.3.**使用Hexo写博客**

----------

&emsp;由于github pages存放的都是静态文件，博客存放的不只是文章内容，还有文章列表、分类、标签、翻页等动态内容，假如每次写完一篇文章都要手动更新博文目录和相关链接信息，相信谁都会疯掉，所以hexo所做的就是将这些md文件都放在本地，每次写完文章后调用写好的命令来批量完成相关页面的生成，然后再将有改动的页面提交到github。

#### &emsp;3.3.1 安装 Hexo
&emsp;1.在自己认为合适的地方创个文件夹，我是在D盘建了一个blog文件夹，然后通过命令行进入到该文件夹里面。
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/GhHHIhI5Fl.png?imageslim)

&emsp;2.输入`npm install hexo -g`，开始安装Hexo。
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/bLBff6a9AF.png?imageslim)

&emsp;3.输入`hexo -v`，检查hexo是否安装成功。
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/D6e5FH9cb0.png?imageslim)

#### &emsp;3.3.2 初始化

&emsp;1.输入`hexo init`，初始化该文件夹（时间会有点久，耐心等待...）看到后面的 “Start blogging with Hexo！”，初始化完成。
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/21AG9c7DLH.png?imageslim)

hexo会自动下载一些文件到这个目录，包括node_modules，目录结构如下图：
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/ACE1b8Gl8a.png?imageslim)

&emsp;2.输入`npm install`，安装所需要的组件。
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/i4lHJ2EDKa.png?imageslim)

&emsp;3.输入`hexo g`，hexo就会在public文件夹生成相关html文件，这些文件将来都是要提交到github去的：
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/7Dk0Ff6170.png?imageslim)

&emsp;4.输入`hexo s`，此命令是开启本地预览服务，打开浏览器访问 http://localhost:4000 即可看到内容。
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/FGH6A2bkAh.png?imageslim)

&emsp;第一次初始化的时候hexo已经帮我们写了一篇名为 Hello World 的文章，默认的主题比较丑，打开时就是这个样子：
![mark](http://p3nn031ge.bkt.clouddn.com/blog/180205/cmE5g9jALA.png?imageslim)


#### &emsp;3.3.3 修改主题

&emsp;个人觉得默认主题有些丑，所以我换了一个好看的主题，并加工，修改成自己想要的样子。

&emsp;1.找到自己喜欢的主题，通过 Git checkout 代码下载。

```java
    cd /f/github/hexo/
    https://github.com/WongMinHo/hexo-theme-miho.git
```
&emsp;2.下载好主题后，修改`_config.yml`中的`theme: landscape`改为`theme: miho`，然后根据主题配置文件进行配置，再重新执行`hexo g`来重新生成。

&emsp;如果出现一些莫名其妙的问题，可以先执行`hexo clean`来清理一下`public`的内容，然后再来重新生成和发布。

&emsp;3.接下来就是根据你自己的爱好，修改所选的主题。

#### &emsp;3.3.4 备份

&emsp;Hexo在发布之后在github的仓库中我们只能找到生成的静态文件，而我们的博客的源文件：主题，文章之类的，都还在本地，并没有备份。这样很危险，万一那天电脑坏了或者是出现一些其他问题，就得从头再来。所以我们可以利用github的分支思想来备份我们的源文件。
&emsp;**1.添加过滤内容**
&emsp;备份的时候我们把master分支放生成的静态文件，Hexo-Blog（此处文件夹必须和存储分支名字一致）放我们要备份的源文件。

&emsp;在项目的根目录下新建Hexo-Blog文件夹，将项目中的文件复制粘贴到刚刚新建的文件夹中，`.deploy_git`、`public`文件夹和我们的master分支内容重复，而`_config.yml`为我们的站点配置文件，安全起见，这个几个文件都不备份。所以，我们在根目录下面建一个`.gitignore`文件来建立“黑名单”。

&emsp;.gitignore文件内容：
```java
    /.deploy_git
    /public  
    /_config.yml
```
&emsp;**2.备份**
&emsp;鼠标右击 Hexo-Blog 文件夹，打开 Git Bash ,依次输入
```java
   $ git init
   $ git remote add origin git@github.com:username/username.github.io.git		
   $ git add .
   $ git commit -m "blog"
   $ git push origin master:Hexo-Blog
```
&emsp;这时，你会发现你的github博客仓库已经有了一个新分支 Hexo-Blog ,备份工作完成。

&emsp;**3.后续**
&emsp;以后，每次在本地写好博文后，可以先执行下列命令进行备份，然后再更新静态文件。
```java	
   $ git add .
   $ git commit -m "blog"
   $ git push origin master:Hexo-Blog
```
#### &emsp;3.3.5 发布

&emsp;1.清空hexo静态文件和缓存，并重新生成
```	
   hexo clean && hexo g 
```
&emsp;2.本地预览，确没有问题再进行发布
```	
   hexo s 
```
&emsp;3.进行发布
```	
   hexo d
```
#### &emsp;3.3.5 效果
&emsp;可以访问我的git博客来查看效果：https://tongliping0709.github.io/
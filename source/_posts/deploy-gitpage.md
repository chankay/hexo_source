---
title: hexo + gitpage 搭建个人博客
date: 2016-09-06 20:25:52
tags: 
---

github的gitpage可以方便的建立个人博客，并且可以绑定自己的域名，基本上能够满足博客的需求，但是gitpage只提供静态化的页面，写一篇博客相当于是要用html去写一个页面，对于一个后端程序员来说很头疼，可能写篇博客大部分的时间都花在了调页面上。程序员们怎么会允许这样的事情发生呢！本文就来介绍下用hexo管理gitpage的流程。
<!--more-->

# 一、gitpage设置
gitpage官方说明如下:
Head over to GitHub and create a new repository named username.github.io, where username is your username (or organization name) on GitHub.
即新建一个项目，项目名为  你的名字.github.io ，（你的名字。。。不是真的就叫“你的名字”）

echo "Hello World" > index.html
git add --all
git commit -m "Initial commit"
git push -u origin master
按照上面步骤新建一个index页面，然后同步到git，再在浏览器打开 你的名字.github.io，就可以访问了。

# 二、hexo安装部署
nodejs
从nodejs官网下载相应的安装包安装nodejs
注意的是: centos 6.8 版本gcc过低，不能源码编译安装nodejs，需安装epel源后通过yum 安装nodejs
rpm -Uvh http://mirrors.aliyun.com/epel/epel-release-latest-6.noarch.rpm　//安装epel源

yum install nodejs npm　//安装nodejs , npm

正式安装hexo，其实很简单啦，也就一条命令的事
npm install -g hexo　//安装hexo
安装完后的配置
hexo init blog　//初始化
cd blog

配置_config.yml
deploy:
     type: git
     repo: git@github.com:你的git名称/你的git名称.github.io.git
     branch: master

在blog目录执行，否则不能部署到git
npm install hexo-deployer-git --save

新建文章
hexo new [layout] <title>
生成的文件默认在source/_post/下，用markdown编辑器直接打开写博客就行。

生成静态页面
hexo generate

部署到github
hexo deploy

# 三、域名解析
如果你觉得github的域名不酷，那么你可以自己去注册一个域名，注册后在域名后台添加一条CNAME解析，解析到
你的名字.github.io，
然后在blog/source/下新增CNAME文件，内容填你自己解析过的域名。
如果只在github设置里面配置，下次deploy的时候会覆盖掉CNAME文件，这时候你会发现你自己的域名不能访问了，然后苦逼的开始寻找原因。。。

# 四、更换电脑后如何配置
白天在公司电脑上配置好了hexo环境，晚上回到家准备写博客时发现hexo部署到github上的只有静态页面文件，hexo的配置等等并没有同步，解决这个问题网上有好多解决方法，有用云盘直接备份hexo目录的，既然用的github，我干脆就直接新建了个git项目，将整个hexo目录放进去同步，目录下的public目录是放生成的静态页面的，直接忽略掉，node_modules是放安装的node模块，也忽略掉，这样在其他电脑上，直接clone一份下来，就可以直接写博客了。




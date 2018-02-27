---
layout: post
title: 笔记Git/Jekyll/Ubuntu/VirtualBox
tags:
  - learning
  - PC
---

近些天从接触GitHub开始，一路摸索得到了如下一些方面的知识：

GitHub作为一个共享开源的平台，也可以用来做个人博客。

使用GitHub Desktop经常产生混乱，至少在我的Windows平台下是这样，下载Git在Windows中使用Git Bash命令行也是个不错的选择。

GitHub建立个人博客主要利用了GitHub提供Pages功能，我个人比较浅的理解是，GitHub后台会自动把用户Repository内的文件，以网页的形式组织并发布。

Jekyll的好处是，提供一堆漂亮的模板可以让初学者很容易开始搭建自己的博客，而且在本地可以预览效果，个人认为这个对于象中国这样网络环境极差的地方尤其有意义。

然而事实并不总是想想象的那样顺利，在我的Windows 7上安装Jekyll简直是一场噩梦，把Ruby也装了，Jekyll终于装上了，却无论如何也无法正常进行Jekyll Serve，没有Jekyll Serve进行预览，我留你又有何用……

Windows上没法用，我用其它操作系统还不行，可吃饭靠Windows的我，不能拿着俩电脑折腾啊，于是又陷入了虚拟机的坑中，VirtualBox，Ubuntu...


## Git

Git将本地和服务器上的文档进行版本和分支管理，它在本地文件夹中产生一个`.git`文件夹，用于记录本地各种变化信息，通过一系列命令，将本地的变化先记录，再上传。最简单的应用如下：

1. 拿来主义


`git clone` 后面加URL，用于把网上别人的repository偷到本地当前目录来


2. 简单修改，定制自己的效果 / 日常更新博客文章

这一步与git命令行无关，自己可以学习网页前端的各种知识，把博客弄得更符合自己的意思。

在日常应用中，这一步用来更新博客文章（通常在`_posts`文件夹下），注意文件名按照原有的文件命名规律。文章前几行三条短横线之间的部分是头信息，通常是一些tag。

3. 告诉git哪些更改是需要它管理的

`git add`通常配合`-A`（注意区分大小写）来使用，把git监控到的更改，确认给git，这些就是需要它管的。

在任何时候，都可以用`git status`来看看当前repository中哪些地方有更改。

4. 准备上传的用户名等信息

`git config user.email`加上以双引号包围的用户邮箱地址，可以告诉git，以哪个用户名进行commit命令的记录。例如：*git config user.email "youremail@github.com"*。此用法仅应用于当前repository，即当前目录。如果一次性指定所有目录的用户名，可以使用`git config --global user.email`。 

5. 确认提交变更

`git commit -m "some text"`确认提交变更，双引号内加入本次提交的备注。

6. 将变更推送至github服务器上

`git push`将变更推送，此处可能提示输入github的用户名密码。

参考别人的图解，以上过程可以图示为：![git illustration][1]


>  - git是据说是Linux大神闭门造出来的
>
>  - GitHub是提供remote repository的网站，并不等同于git
>
>  - GitHub提供图形化的GitHub Desktop来管理，但实际效果不好，下载git bash使用命令行更实用

## GitHub

GitHub作为一个存放开源共享文档的网站，使用并不困难。之于利用它建立个人博客，我有如下几点需要记录下来。

GitHub本来是被设计为一个remote repository的，它提供的一个“额外”功能是Page，个人博客是利用这个额外功能。过去，GitHub识别哪个repository是Page是靠repository的name的，默认username.github.io这个repository会被GitHub解释为page。现在，GitHub提供了更灵活的方案，用户可以把任意名字的repository，通过setting，设置其为Page。该Repository的内容，会以Jekyll的方式被转换成网页，地址在设置成Page以后，会出现在setting界面里。任何人在浏览器中输入这个地址，都可以访问到该repository被转换成的网页。

一个目前我还没完全明白的地方，username.github.io这个Page和其它Page的关系是什么？貌似其它Page里面点击Home，会回到这个.io的Page？没搞清楚这是GitHub的缺省解释方式？还是由于我fork的别人的模板恰好设置了Home指向.io？

## Jekyll

我的理解Jekyll是一个解释器，一个按照既定的protocol把用户的一堆文件夹以及里面的文件解释成一个网站并提供本地的访问。

GitHub使用Jekyll来解释其提供的Page功能的repository内的文件。

Ubuntu下直接可以安装Jekyll。

`jekyll serve -d <path>`可以把当前目录下的所有内容在destination folder path下生成网站，并运行用户访问local host来预览网站内容

## VirtualBox

VirtualBox是开源的虚拟机软件。

Guest machine - 指虚拟机模拟出来的主机
Host machine - 指VirtualBox安装于上的物理计算机

### 安装操作系统

首先需要下载一个操作系统的.iso文件，然后在VirtualBox中新建一个Guest machine，并在属性中加载.iso文件至Guest的光驱，然后启动虚拟机，一步步安装操作系统。


### 如果出现花屏

在VirtualBox里安装Lubuntu操作系统时，会出现花屏，此时等待Guest虚拟机的硬盘不怎么转时（Guest窗口下面有硬盘读写图标），按right Ctrl \+ F1切换至命令行窗口，再次按right Ctrl \+ F7切换至图形窗口即可。

### Guest和Host之间的信息交换和文件共享

为了Guest和Host之间交换信息，非常有必要安装Guest Additions。

#### 准备工作

虚拟机里先安装一些virtualbox相关的软件

> sudo apt install build-essential and linux-headers-virtual
>
> sudo apt install virtualbox-dkms

#### 安装Guest Additions

在虚拟机窗口的下拉菜单中加载光盘Insert Guest Additions CD image，然后在Guest machine里面使用光盘安装。光盘根目录下有安装方法。

安装过程中，出现modprob vboxsf failed，查了很多资料，没能解决掉这个错误，但最后仍可以使用Share Folder功能。重启后，VirtualBox也提示Guest Additions do not appear to be available，但仍不影响Share Folder的功能。

#### 配置

- VirtualBox下拉菜单或是属性中可以设置Share Folder。不明白为什么有两个设置，一个Machine Folders，一个Transient Folders。无论如何，点旁边带加号的图标，可以设置一个Host machine内的文件夹路径。

- Guest machine里面，用户如果要访问Share Folder，需要在一个组里

> sudo usermod -aG vboxsf userName

## Ubuntu

我使用的是Lubuntu，一个轻量的Ubuntu。每次安装完后，要做如下基本设置：

### apt application repository source

更新一个比较快的repository source。在Software update center中选择中国区，让系统测试比较快的服务器。

### 中文输入法

Preference，Language Support，不要check and download incomplete language packages。

点击Install / Remove Language ...，安装Chinese。

log off then log on

Preference，Language Support，把input method system改成fcitx

log off then log on again

现在系统托盘应该出现小企鹅标志了。Preference，fcitx configuration，去掉only show current language前面的勾，中文输入法应该显示在列表中了，

### 分辨率

虚拟机分辨率很低，可以安装如下：

> sudo apt-get install virtualbox-guest-dkms

### 常用命令

> printenv 显示系统变量
>
> sudo -i 临时切换至root
>
> sudo reboot
>
> uname -r 显示linux版本


[1]: https://wx2.sinaimg.cn/mw1024/6e471a1dgy1forj1s16ulj20s50f03zr.jpg 
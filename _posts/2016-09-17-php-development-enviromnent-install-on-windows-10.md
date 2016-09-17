---
layout:     post
title:      "如何搭建基于 Windows 10 的 PHP 开发环境？"
date:       2016-09-17 20:41:28 +0800
author:     "ranwuer"
categories: work
tags: php win10 dev-environment

excerpt: 主要总结了php在windows10下开发环境的建立过程（正确的姿势）
---

PHP 开发环境的搭建想必是每位开发者都必须经历的过程。目前来说，国内众多大大小小的公司使用 Windows 作为开发环境毕竟占多数，
那些配了 Mac 的公司毕竟还是比较小众。本文章主要记录了我在 Windows 环境下搭建开发环境的一些经验总结。

### 环境介绍
主要用到了4个软件，这里介绍一下 Laragon。Laragon 是一个 Windows 下的 PHP 集成安装包。类似于 wamp 和 xampp。这些软件
都可以较为容易的安装 PHP 开发环境。

为什么要用 Laragon？主要是因为在使用 PhpStorm 有些功能的时候需要一个本地 PHP 运行环境，所以 Laragon 可以很好的管理
在本地安装的所有 PHP 相关软件。

Vagrant 和 VirtualBox 都是用来运行 Linux 虚拟机的。以应付某些 Windows 解决
不了的场景。

```
1. Windows 10
2. Vagrant
3. VirtualBox
4. Laragon
5. PHPStorm
6. Homestead
```

### 安装过程
以下安装过程都是默认安装，也就是点击下一步直到安装完成。

1. 下载 [Vagrant](https://releases.hashicorp.com/vagrant/1.8.5/vagrant_1.8.5.msi) 并安装。
2. 下载 [VirtualBox](https://www.virtualbox.org/wiki/Downloads) 并安装。
3. 下载 [Laragon](https://laragon.org/) 并安装。
4. 下载 [PHPStorm](https://www.jetbrains.com/phpstorm/) 并安装。

### 配置过程
由于我主要使用 Yii 框架来开发 PHP 程序，所以这里介绍一下 Yii 开发环境的部署
方式。

以下操作都是用的 [cmder](http://cmder.net/) 命令行工具。启动方式为：打开 Laragon， 在面板中选择
 Terminal。

**1. 安装虚拟运行环境**

Homestead 是 Laravel 官方的一个基于 Vagrant 的开发环境，配置都非常方便。

>安装 Homestead Vagrant box

```
vagrant box add laravel/homestead
```
这条命令在 Vagrant 安装完毕后即可使用。如果有梯子的话，可以开启全局模式，这样
以来下载速度会非常快。如果没有梯子，也可以下载，只不过速度没有它快。

>安装 Homestead

安装 Homestead 只需要克隆一下这个项目即可。这个 Homestead 在你的家目录，Homestead
box 就是从这个目录启动。

```
cd ~
git clone https://github.com/laravel/homestead.git Homestead
```

然后进入 Homestead 目录，并运行`bash init.sh`命令来生成`Homestead.yaml`配置
文件。这个`Homestead.yaml`配置文件会放在`~/.homestead`隐藏目录下。

```
bash init.sh
```

>配置 Homestead.yaml文件

首先打开`~/.homestead`目录下的`Homestead.yaml`文件。

修改共享目录：

```
folders:
    - map: C:\laragon\www
      to: /home/vagrant/Code
```
`map`所对应的内容可以改为 Windows 下的任意目录，自己方便就行。

修改网站域名和根目录：

```
sites:
    - map: yiis.dev
      to: /home/vagrant/Code/basic/web
```
`map`所对应的内容为网站域名，可以修改为你喜欢的任意名称，但建议以不常见
后缀结尾为佳。比如开发的话，就用`.dev`。

`to`所对应的内容是网站的根目录，也就是说我从浏览器打开`yiis.dev`后马上访问到这个目录的文件。

`basic`为 yii 的项目名称。

>修改 hosts 文件

打开 Laragon，在面板中选择如下图所示的位置：
![laragonHosts](/photo/laragonHosts.png)

然后打开了 hosts 文件，加入以下内容：

```
192.168.10.10   yiis.dev
```

这里的域名要和`sites`里的域名一样。

>启动 Homestead

打开 cmder， 进入用户根目录：
```
cd~ #没有空格
```

然后进入 Homestead 目录：
```
cd Homestead
```

输入：
```
vagrant up
```
启动即将开始。

**2. 安装 Yii 项目文件**

打开 cmder，进入`C:\laragon\www`目录。

修改 composer 镜像源：

```
composer config -g repo.packagist composer https://packagist.phpcomposer.com
```

查看修改情况：
```
composer config -gl
```
![composerMirror](/photo/composerMirror.png)

安装 Yii 框架
```
composer global require "fxp/composer-asset-plugin:^1.2.0"
composer create-project --prefer-dist yiisoft/yii2-app-basic basic
```
运行完毕后会在`C:\laragon\www`目录下看到一个`basic`目录，就是我们创建的一个
Yii 项目了。

然后在浏览器中输入`yiis.dev`查看效果
![yiisStarted](/photo/yiisStarted.png)

如果没有看到预期的效果。请仔细检查`sites`配置区域。一般来说，yii 的
网站根目录是在`web`目录下，也就是说，配置的时候必须跟上绝对路径到`web`目录位置。比如，
`/home/vagrant/Code/basic/web`。像 Laravel 项目的网站根目录是在`public`文件下，可以
根据这个原理配置相应目录。

**3. 配置 PHPStorm**

为了提高开发效率，充分利用 PHPStorm 的辅助功能是不错的选择。（未完）
---
layout: post
title:  "在CentOS7中配置Ruby环境"
date:   2016-07-14 01:07:33 +0800
categories: work
tags: ruby, ruby on rails, nodejs
excerpt: 本文主要介绍了Ruby on Rails在Centos7环境下的搭建，主要运用了rbenv来管理和安装ruby。同时也介绍了Nodejs的安装方法，主要参考了官方的安装方法，使用nvm来管理和安装Nodejs，也是非常简单的，希望对大家有用！
---

## 安装rbenv
安装rbenv是来控制ruby的版本，非常方便。

运行以下代码来安装基本依赖环境：
{% highlight shell %}
sudo yum install -y git-core zlib zlib-devel gcc-c++ patch readline readline-devel libyaml-devel libffi-devel openssl-devel make bzip2 autoconf automake libtool bison curl sqlite-devel
{% endhighlight %}

以最简单的方式安装rbenv：
{% highlight shell %}
cd
git clone git://github.com/sstephenson/rbenv.git .rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile
echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
source ~/.bash_profile

git clone git://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bash_profile
source ~/.bash_profile
{% endhighlight %}

这些命令会将rbenv安装到家目录。

现在可以安装ruby了。

## 安装Ruby
可以自己决定安装哪个版本的ruby，安装多个版本的ruby也可以，可以用rbenv来自由切换ruby的版本。

下面安装ruby的最新版：
{% highlight shell %}
rbenv install -v 2.3.1
rbenv global 2.3.1
{% endhighlight %}

`global`命令设置ruby的默认版本。如果想指定任意版本为默认版本，那么请运行这个命令。

验证ruby的版本：
{% highlight shell %}
ruby -v
{% endhighlight %}

更换`gem`源：
{% highlight shell %}
gem sources --add https://ruby.taobao.org/ --remove https://rubygems.org/
gem sources -l
*** CURRENT SOURCES ***

https://ruby.taobao.org
{% endhighlight %}

在安装`gem`的时候，`Rubygems`默认会为每个`gem`生成本地文档，然而这将花费大量时间，建议是关闭它：

{% highlight shell %}
echo "gem: --no-document" > ~/.gemrc
{% endhighlight %}

安装`bundler gem`来管理应用依赖：
{% highlight shell %}
gem install bundler
{% endhighlight%}

## 安装Rails
安装`rails 5.0`
{% highlight shell %}
gem install rails -v 5.0.0
{% endhighlight%}

如果你安装了新版本的`Ruby`或包含命令`gem`，那么需要执行`rehash`子命令，作用是为所有被`rbenv`所知道的`Ruby`命令安装中间件（shims）：
{% highlight shell %}
rbenv rehash
{% endhighlight%}

查看`rails`的版本
{% highlight shell %}
rails -v
{% endhighlight%}

## 安装JavaScript运行时环境
有些`Rails`功能需要JavaScript运行环境，比如`Asset Pipeline`。

安装nvm
: Node Version Manager，管理`Nodejs`的版本（推荐的做法）

{% highlight shell %}
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.3/install.sh | bash
source ~/.bashrc
{% endhighlight%}

检验是否安装成功
{% highlight shell %}
command -v nvm

//nvm --version 查看版本号
{% endhighlight%}
当敲完上面的字符后，如果输出`nvm`，说明安装成功。

安装最新版的`Nodejs`：
{% highlight shell %}
nvm install node

//或者安装特定版本的node
nvm install node 4.4.7
{% endhighlight%}

使用此版本的`node`
{% highlight shell %}
nvm use node

//或者使用特定版本的node
nvm use node 4.4.7
{% endhighlight%}

查看`Nodejs`版本号
{% highlight shell %}
node -v
{% endhighlight%}


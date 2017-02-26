---
layout: post
title: Jekyll 在本地以及 GitHub Pages 上的部署方法
---

因为今天需要迁移多篇已经发在微信公众号的文章，所以就在本地对 Jekyll 进行了环境部署，方便批量修改与提交。Fork Jekyll 快有一年的时间了，自己 GitHub 仓库上的版本还是 1.0 而最新的 Jekyll 已经升级到了 3.0.1，对比来看，变化还是比较大的，所以就直接新建了一个基础项目，然后将内容进行了迁移。

整个过程下来，大概进行了以下几个步骤：
  
1. Ruby 运行环境安装
2. Gem 安装
3. Jekyll gem 安装
4. github-pages gem 安装
5. bundle 安装
 
## Ruby 运行环境安装

这一步不用多说，下载地址：[Installing Ruby](https://www.ruby-lang.org/en/documentation/installation/)

## Gem 安装
Gem 是 Ruby 的包管理框架，用来下载依赖。
下载地址：[Download RubyGems](https://rubygems.org/pages/download)

下载后需要用终端进行安装，Windows 下可以用 PowerShell。

## Jekyll gem 安装

使用以下命令安装：

$ gem install jekyll

安装完成后用：

$ jekyll new myblog

该命令会新建 myblog 文件夹，然后将 Jekyll 的基础文件放在里面。

## github-pages gem 安装

使用以下命令安装：

$ gem install github-pages

内容比较多，安装时间较长。

## bundle 安装

bundle 是 Ruby 下用来确保项目一致性的工具，具体可参见[官网](http://bundler.io/)。

使用以下命令安装：

$ gem install bundler

安装完成以后，需要在你的项目根目录下建立 Gemfile 文件，文件名为 Gemfile，不要后缀名。

内容为：

source 'https://rubygems.org'
gem 'github-pages'

然后使用：

$ bundle install

进行依赖安装，但其实我们已经预先安装好了 github-pages，之所以这么做是因为国内的网络环境。

官方说明：

* [GitHub Pages](http://jekyllrb.com/docs/github-pages/)

* [Using Jekyll with Pages](https://help.github.com/articles/using-jekyll-with-pages/)

然后在本地进行测试：

$ bundle exec jekyll serve

----------------

在这些步骤完成以后，在你的 GitHub 上新建一个 username.github.io 为名的仓库，然后 push 内容即可。（username 即你的用户名）

具体细节可以参考：[GitHub Pages Basics](https://help.github.com/categories/github-pages-basics/)



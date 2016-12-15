---
layout: post
title: OS X配置Ruby环境
date: 2016-02-29 23:33
author: kojirou
comments: true
categories: [macOS]
---
步骤1 － 安装 RVM

$ curl -L https://get.rvm.io | bash -s stable

载入 RVM 环境（新开 Termal 就不用这么做了，会自动重新载入的）
$ source ~/.rvm/scripts/rvm

检查是否安装正确
$ rvm -v

步骤2 － 用 RVM 安装 Ruby 环境

列出已知的ruby版本
$ rvm list known

可以选择现有的rvm版本来进行安装（下面以rvm 2.0.0版本的安装为例）
$ rvm install 2.0.0

等待

查询已经安装的ruby
$ rvm list

卸载一个已安装版本
$ rvm remove 1.9.2


步骤3 － 设置 Ruby 版本

RVM 装好以后，需要执行下面的命令将指定版本的 Ruby 设置为系统默认版本
$ rvm 2.0.0 --default

同样，也可以用其他版本号，前提是你有用 rvm install 安装过那个版本

这个时候你可以测试是否正确
$ ruby -v
ruby 2.0.0p247 (2013-06-27 revision 41674) [x86_64-darwin13.0.0]

$ gem -v
2.1.6

这有可能是因为Ruby的默认源使用的是cocoapods.org，国内访问这个网址有时候会有问题，网上的一种解决方案是将远替换成淘宝的，替换方式如下：
$gem source -r https://rubygems.org/
$ gem source -a https://ruby.taobao.org

要想验证是否替换成功了，可以执行：
$ gem sources -l

正常的输出结果：
　　　　　　CURRENT SOURCES　　　　　　　　　　　　

　　　　　　http://ruby.taobao.org/　　　　　　　　　　　　

到这里就已经把Ruby环境成功的安装到了Mac OS X上，接下来就可以进行相应的开发使用了。

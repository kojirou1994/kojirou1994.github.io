---
layout: post
title: 安装Shadowsocks并用Polipo转换成HTTP代理
date: 2016-05-09 01:56
author: kojirou
comments: true
categories: [Shadowsocks]
---
<h3>Pip安装</h3>

安装pip
<code>apt-get install python-pip</code>
安装ss
<code>pip install shadowsocks</code>
安装polipo
<code>apt-get install polipo</code>
ss要使用chacha20要安装libsodium

<pre><code>#!/bin/bash
sudo add-apt-repository ppa:chris-lea/libsodium;
sudo echo "deb http://ppa.launchpad.net/chris-lea/libsodium/ubuntu trusty main" &gt;&gt; /etc/apt/sources.list;
sudo echo "deb-src http://ppa.launchpad.net/chris-lea/libsodium/ubuntu trusty main" &gt;&gt; /etc/apt/sources.list;
sudo apt-get update &amp;&amp; sudo apt-get install libsodium-dev;
</code></pre>

sslocal启动ss

<pre><code>sslocal -p 61010 -k password -d start
# or
sslocal -c config -d start
</code></pre>

<h3>Debian/Ubuntu</h3>

First, add the GPG public key to your system:
<code>$ wget -O- http://shadowsocks.org/debian/1D27208A.gpg | sudo apt-key add -</code>
Install the binaries by adding each of the following repositories to your system.
On Debian Wheezy, Ubuntu 12.04 or any distribution with libssl > 1.0.0
<code>$ echo "deb http://shadowsocks.org/debian wheezy main" &gt;&gt; /etc/apt/sources.list</code>
On Debian Squeeze, Ubuntu 11.04, or any distribution with libssl > 0.9.8, but &lt; 1.0.0
<code>$ echo "deb http://shadowsocks.org/debian squeeze main" &gt;&gt; /etc/apt/sources.list</code>
Then

<pre><code>$ apt-get update
$ apt-get install shadowsocks-libev
</code></pre>

<h3>Github</h3>

<pre><code>$ git clone https://github.com/shadowsocks/shadowsocks-libev.git
$ cd shadowsocks-libev
$ sudo apt-get install build-essential autoconf libtool libssl-dev
$ ./configure &amp;&amp; make
$ make install
</code></pre>

<h3>配置Polipo</h3>

polipo配置文件目录: /etc/polipo/
配置文件加上一行
<code>socksParentProxy=localhost:1080</code>
polipo默认端口为8123
修改完后重启polipo
<code>/etc/init.d/polipo restart</code>

<h3>Example</h3>

<pre><code>http_proxy=http://localhost:8123 apt-get update

http_proxy=http://localhost:8123 curl www.google.com

http_proxy=http://localhost:8123 wget www.google.com

git config --global http.proxy 127.0.0.1:8123
git clone https://github.com/xxx/xxx.git
git xxx
git xxx
git config --global --unset-all http.proxy
</code></pre>

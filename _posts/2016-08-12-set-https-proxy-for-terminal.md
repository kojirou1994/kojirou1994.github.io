---
layout: post
title: 为常用软件设置代理
date: 2016-08-12 11:18
author: kojirou
comments: true
categories: [未分类]
---
<strong>为ssh设置https代理</strong>

1.安装corkscrew
brew install corkscrew
2.新建ssh设置文件
touch ~/.ssh/config
3.编辑config文件

<pre><code>Host github.com
HostName ssh.github.com
port 443
ProxyCommand /usr/local/bin/corkscrew 127.0.0.1 8888 %h %p
</code></pre>

<strong>为npm设置http(s)代理</strong>

<pre><code>npm config set registry http://registry.npmjs.org/
npm config set http-proxy http://username:password@ip:port
npm config set https-proxy http://username:password@ip:port
npm set strict-ssl false
#check settings:
npm config list
</code></pre>

<strong>为git设置http代理</strong>

<pre><code>#设置代理
git config --global http.proxy 127.0.0.1:8123
#取消代理
git config --global --unset-all http.proxy
</code></pre>

<strong>为终端设置http代理</strong>
编辑.zshrc

<pre><code>export https_proxy=http://127.0.0.1:8888
export http_proxy=http://127.0.0.1:8888
</code></pre>

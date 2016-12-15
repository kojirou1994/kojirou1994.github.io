---
layout: post
title: 解决Wordpress反复提示更新翻译
date: 2016-05-03 00:20
author: kojirou
comments: true
categories: [未分类]
---
<img src="http://blog.putotyra.com/wp-content/uploads/2016/05/71fb307ajw1en28dgv6ssj20ce076aa2-300x174.jpg" alt="wordpress_update2" width="300" height="174" class="alignnone size-medium wp-image-38" />

<img src="http://blog.putotyra.com/wp-content/uploads/2016/05/71fb307ajw1en28djnedzj20fi0ak0t9-300x204.jpg" alt="wordpress_update" width="300" height="204" class="alignnone size-medium wp-image-39" />
php.ini里面禁用了scandir()函数，把scandir从disable_functions里面删掉就好了.

---
layout: post
title: 在linux下修改编译网件WNDR3700v4的Openwrt固件，支持128MB NAND
date: 2016-05-02 17:03
author: kojirou
comments: true
categories: [未分类]
---
Openwrt官方的网件WNDR3700v4固件（15.05.1）不能完整利用128MB NAND的空间，刷完后只剩13MB了，网上说还有96MB左右空闲着，只能修改Makefile自己重新编译固件，在linux编译环境下非常轻松。
一、下载源码包：
wget https://downloads.openwrt.org/chaos_calmer/15.05.1/ar71xx/nand/OpenWrt-ImageBuilder-15.05.1-ar71xx-nand.Linux-x86_64.tar.bz2
下载完成后解压得到：
OpenWrt-ImageBuilder-15.05.1-ar71xx-nand.Linux-x86_64
进入目录：
cd OpenWrt-ImageBuilder-15.05.1-ar71xx-nand.Linux-x86_64
二、修改Makefile文件（红字部份）：
进入该文件夹 target/linux/ar71xx/image/ 修改Makefile文件：
在linux下修改编译网件WNDR3700v4的Openwrt固件，支持128MB <wbr>NAND
三、编译：
make image PROFILE=WNDR4300
若要生成luci 界面请用下面的命令：
make image PROFILE=WNDR4300 PACKAGES="base-files busybox dnsmasq dropbear firewall fstools hostapd-common ip6tables iptables iw iwinfo jshn jsonfilter kernel kmod-ath kmod-ath9k kmod-ath9k-common kmod-cfg80211 kmod-crypto-aes kmod-crypto-arc4 kmod-crypto-core kmod-gpio-button-hotplug kmod-ip6tables kmod-ipt-conntrack kmod-ipt-core kmod-ipt-nat kmod-ipv6 kmod-ledtrig-usbdev kmod-lib-crc-ccitt kmod-mac80211 kmod-nls-base kmod-ppp kmod-pppoe kmod-pppox kmod-slhc kmod-usb-core kmod-usb-ohci kmod-usb2 libblobmsg-json libc libgcc libip4tc libip6tc libiwinfo libiwinfo-lua libjson-c libjson-script liblua libnl-tiny libubox libubus libubus-lua libuci libuci-lua libxtables lua luci luci-app-firewall luci-base luci-lib-nixio luci-mod-admin-full luci-proto-ipv6 luci-proto-ppp luci-theme-bootstrap mtd netifd odhcp6c odhcpd opkg ppp ppp-mod-pppoe procd procd-nand swconfig ubi-utils uboot-envtools ubox ubus ubusd uci uhttpd uhttpd-mod-ubus wpad-mini"
在bin/ar71xx目录下生成4300 和3700v4的固件，以下是wndr3700v4的：
openwrt-15.05.1-ar71xx-nand-wndr3700v4-squashfs-sysupgrade.tar （下载）
和
openwrt-15.05.1-ar71xx-nand-wndr3700v4-ubi-factory.img （下载）
四、刷机：
1.用luci web刷tar包
 亲测用sysupgrade.tar 是不能更改官方分区大小的，如果想增大空间，用第2种方法。
2.用tftp刷img镜像文件
tftp的使用请参考：http://blog.sina.com.cn/s/blog_5f66526e0102wfzi.html
最后上张图：
在linux下修改编译网件WNDR3700v4的Openwrt固件，支持128MB <wbr>NAND

注：如果没有5G的wifi，按电源开关断电，然后再通电，启动就好了。

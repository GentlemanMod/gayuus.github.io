---
layout: post
title:  linux上安装windows系统
date:   2014-01-04 14:08:42
category: "windows"
---
<h2 id="tagline">Linux使用ms-sys引导U盘安装windows</h2>

<p>首先，直接 dd if=win7.iso of=/dev/sdb 是不行的，</p>
<p>其次，grub2 的 loopback 功能对Win7的ISO不起作用（loopback 只支持iso9660格式的光盘镜像），于是没有办法像linux启动盘那样配置一下grub.cfg，放个linux的ISO镜像那么简单明快。</p>

<p><strong>事前准备：</strong>需要gparted、ms-sys、win7安装用ISO，4G及以上大小U盘一个</p>

<p>1.用gparted在U盘上建立一个ntfs分区，编辑flag，<br>
勾上boot选项。这个分区是用来存放win7iso的内容的，所以大小一定要够大，boot选项也就是设为活动分区的意思。</p>
<p>2.挂载win7.iso和新建的ntfs分区，并将全部内容复制到那个ntfs分区。</p>
<p>3.编译安装ms-sys<br>
ms-sys是一个写mbr的工具，起到让系统知道能够引导win7安装的作用，至关重要：http://ms-sys.sourceforge.net
安装就是make，会在代码目录下生成 bin/目录, cd 到 bin/目录下</p>
<p>4.运行：<b>ms-sys -7 /dev/sdX</b><br>
写入mbr。其中的-7参数指win7, sdX指的是U盘对应的盘符（一般为 sdb）
这样就搞定了，注意XP的安装盘是不可以这么做的。

<p>重启，U盘启动，安装系统（需要事先保证有或能有空闲的主分区用于安装Win7）即可。</p>
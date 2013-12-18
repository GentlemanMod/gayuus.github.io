---
layout: post
title:  结束占用adb端口的进程
date:   2013-12-18 12:51:03
category: "Android"
---

<h2 id="tagline">在Windows上，经常会有各种流氓占用adb的端口，我们需要做的就是杀死他</h2>

<pre>
adb server is out of date.  killing...
ADB server didn't ACK
* failed to start daemon *
error: unknown host service
</pre>

<p>当我们使用adb时，如果出现上面的错误时，使用adb kill-server是没有用的。不过我们可以通过cmd和任务管理器来解决掉端口占用这个问题。</p>
<p>打开CMD(Win+R键，然后输入CMD)，输入<strong>netstat -ano | findstr "5037"</strong>，显示出下列进程</p>

<pre>
  TCP    127.0.0.1:5037         0.0.0.0:0              LISTENING       3772
  TCP    127.0.0.1:5037         127.0.0.1:57306        TIME_WAIT       0
  TCP    127.0.0.1:57306        127.0.0.1:5037         TIME_WAIT       0
</pre>

<p>这时候可以看出是“3772”这个进程占用了端口，我们接下来要做的就是将他杀死，再次输入<strong>TASKLIST | findstr "3772"</strong>，就会显示占用端口的进程名称</p>

<pre>
shuame_helper.exe             3772 Console                    3      4,968 K
</pre>

<p>可以看出我的端口是被一个叫“shuame_helper.exe”的进程占用了，用任务管理器把它杀死。然后你该干啥就干啥~</p>
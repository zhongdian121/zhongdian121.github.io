---
layout: post
keywords: blog
description: blog
title: "在Windows上快速搭建Github使用环境的教程"
categories: [琐碎]
tags: [Archive]
group: archive
icon: file-o
---


#Win上快速进入Github的教程

这篇教程很大意义上是为了吸引新程序猿张耀尹入坑写的。由于最近我用Windows的频率越来越少了。写一下备忘也是好的。

###下载和安装git-scm
你可以到[git-scm](http://git-scm.com/download/win)下载一个简单粗暴的windows客户端。下载完成后按next，但别按过火。事实上你按下三个next之后，会提醒你Adjusting your PATH environment。这里我们选择第二个。如此就不需要我们自己手动修改PATH了。

安装完成后同时按下Win+R，输入cmd，在弹出的黑窗口中输入git，有一大段洋文。你就安装对了。

###从github上克隆项目

我们先登录我们的github，点击右上角的加号，create new repository，随便填写些什么。完成之后进入项目，注意右侧有个HTTPS clone URL，复制框内的url。这里我的是https://github.com/zhongdian121/CSharpCollect.git。

之后在cmd中输入以下指令

	cd Desktop
	git clone https://github.com/zhongdian121/CSharpCollect.git

你就会发现远程的程序下载到你的电脑里面了。

###修改远程的项目

我们在刚刚下载下来的文件夹内新建一个文本文件，比如test.txt，再到cmd里面输入

	git status

系统会显示

	On branch master
	Your branch is up-to-date with 'origin/master'.

	Changes not staged for commit:
  	(use "git add/rm <file>..." to update what will be committed)
  	(use "git checkout -- <file>..." to discard changes in working directory)

        test.txt

	no changes added to commit (use "git add" and/or "git commit -a")

看到test.txt，那就对了。我们接下来要把这个保存到服务器。但是首先得让服务器知道我们是谁。在cmd输入：

	git config --global user.email "Github用户名"
	git add .
	git commit -m "对本次修改的评论"
	git push origin

这时候会要求你输入用户名密码，你输入之后，自然就成功了。登录github，你会发现刚刚的文件已经同步到服务器了。

###我不想每次都输入用户名密码

如果你不想每次都输入用户名密码，你应该采用ssh方式上传和下载。参见[Github SSH设置](http://blog.csdn.net/keyboardota/article/details/7603630)
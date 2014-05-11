---
layout: post
keywords: blog
description: blog
title: "Phonegap上的JQuery Mobile"
categories: [前端开发]
tags: [Archive]
group: archive
icon: file-o
---


<h2>Phonegap的目录树结构</h2>
bin,assets,res这些文件夹已经再熟悉不过，libs之类又不多用，这里就直接略过吧。<br />
src文件夹里面的java文件包括了许多初始的设置：<br />
<code>super.setIntegerProperty("splashscreen", R.drawable.splash_sn);
super.setIntegerProperty("loadUrlTimeoutValue", 60000); // 3s后splash关闭
super.loadUrl("file:///android_asset/www/index.html", 3000);   //设置了首次加载的页面（貌似这里的file协议使得跨域调用成为可能，这是后话。
</code>
根目录下的AndroidManifest.xml则提供了一些安装时的系统级的设置，以下的xml标签就是安装程序时提到的需要用的系统功能

<code>
uses-permission android:name="android.permission.READ_CONTACTS" 
uses-permission android:name="android.permission.WRITE_CONTACTS"
uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" </code>

<h2>JQuery Mobile一些基础</h2>
JQM的很多概念和appFramework都差不多，不过以防后面要用到，这里还是记载一下子吧。<br />
<code> meta name="viewport" content="width=device-width" </code>
这段代码使得页面宽度和移动设备宽度统一。<br />
最常用到的属性，一是div标签中的data-role="page","header","content","footer"。二是超链接a标签中的data-rel="back","dialog"；href="#page1"；data-transition="pop","slide","flow"....等等。<br />
a标签可以用来直接充当按钮，只需要用到data-role="button"属性，同时a元素也拥有其他一些属性，比如data-inline="true"使得按钮不用占一整行而仅仅占用拥有的字符宽度。data-mini="ture"使得按钮比较扁，data-theme="b"可以指定按钮甚至其他页面元素的样式，data-icon="arrow"可以在按钮中使用图标，data-iconpos="left"可以指定按钮中图标和文字的相对位置，disable=""可以让按钮无法点击。对于div标签，如果应用data-role="controlgroup" data-type="horizontal"可以创建水平按钮组。 <br />
完全可以通过修改css文件，自定义整个主题。<br />


<h2>JQuery Mobile插件</h2>
图片滑动浏览 PhotoSwipe <br />
图片幻灯片 Camera <br />
滚动选择时间 Mobiscroll <br />
搜索插件 AutoComplete <br />
日期对话框 DateBox <br />
简单对话框 SimpleDialog <br />
快捷标签 ActionSheet <br />
下拉更新 iscroll.js <br />
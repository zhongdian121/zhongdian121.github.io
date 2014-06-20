---
layout: post
keywords: blog
description: blog
title: "微人大服务中心phonegap项目开发备忘"
categories: [前端开发]
tags: [Archive]
group: archive
icon: file-o
---


由于这个项目花了很长的时间，所以我还是把这个写成一个流水账吧。
<h1>关于整体项目设计</h1>
<ul>
<li><strong>首先是各种命名缺乏规范。</strong>大类上，包括js的函数和变量的命名、html里面每个class和id怎么命名的。分小了说，js的变量，全局和局部在命名上怎么区别。html里面class有panel下级的命名，还有莫名其妙的其他位置的命名。介于目前也没有形成完整的约束。这里还是形成自己风格吧。js的方法（函数）都用骆驼命名法，例如getUserPic()。对于js的局部变量命名不必多加注意，由于很多是直接和html的id绑定的，不妨两者同步。js全局变量用帕斯卡命名法。前面用大写字母构成命名空间:LISTRefreash。html方面，id用帕斯卡命名法，class用骆驼命名法。有时候要标明属于哪个大框架（比如panel），在前面加上框架名加下划线：Detail_SponsorName，这是个id，detail_sponsorName这是个类。</li>
<li>这个项目各个功能确实对我都很新鲜，每走一步都觉得新奇，但是也就是这样，缺乏整体的成竹在胸。<strong>以后做项目，一定要在需求设计阶段把整个功能过一遍。</strong>现在这样面对一个问题单独解决，真的太业余，不能联系起来看矛盾，一种措手不及的感觉！</li>
</ul>

<h1>关于html和css</h1>
<ul>
<li><strong>首先我没有搞清楚垂直方向上的居中问题。</strong></li>
<li><strong>整个页面哪个地方用比例布局，哪个地方用绝对像素布局，一开始我并没有大的方向。</strong></li>
<li>css广泛应用了相对定位的选择器，这样是很好的，但是由于一开始对html的结构把握不足，导致修改之后样式奇怪的行为。此外，<strong>css的重用性现在也太低啦。</strong>这些都跟html结构，甚至命名规范有关。</li>
</ul>

<h1>关于javascript</h1>
<ul>
<li>或许最明显的就是<strong>整个js面向对象的写法几乎为0！</strong></li>
<li><strong>页面之内穿参数竟然依赖于全局变量，调用函数也是连珠炮……</strong></li>
</ul>

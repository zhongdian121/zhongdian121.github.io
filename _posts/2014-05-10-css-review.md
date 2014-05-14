---
layout: post
keywords: blog
description: blog
title: "设计师高度的css学习"
categories: [前端开发]
tags: [Archive]
group: archive
icon: file-o
---


<h2>曾经遗漏的HTML知识</h2>
<del>HTML支持自定义标签，虽然对于大多数浏览器可以直接自己猜测标签的意思，但是官方的做法还是在html开标签的时候，后面加上xlmns属性，加上自定义名字空间的名字作为它的值。“html xmlns:article“这样就定义了一个名字叫article的名字空间。然后可以用“article:文章正文”方式定义一系列自定义标签。这里面涉及到css时还要必须在名字空间后加／，相当麻烦，如无必要，还是不要用了。</del><br />
<cite>对于上文的自定义标签，完全可以使用div加上类名来实现。不过这样做却会受到认为html标签应当为语义服务而非形式服务的纯粹论者质疑。</cite>
title标签和h1标签往往是搜索引擎抓取关键词的地方。be aware!<br />

<h2>css中容易混淆忽略的基础</h2>
<ul>
<li>泛上下文选择符只需要在标签中加空格。严格的子选择符则是>号。一般同胞选择符是～号，近邻同胞是＋号。通配符＊可以用来选择孙子元素。不要在标签中滥用类，并且为每个类写css。实际上，基于继承和上下文选择的css代码维护量将更少。</li>>
<li>此外还有一些很好玩的选择符。我们如果知道某个属性的存在可以使用属性名选择符。比如<code>img[title] {border:2px;}</code>。此外甚至可以限定其属性值用来匹配。比如[title="me"]。<del>搞笑的是，这个发明了之后要id选择器和类选择器干嘛？</del></li>>
<li>此外就是伪类了。需要注意的是链接必须要按照LoVe?HA!的顺序写，也就是link, visited, hover, active。此外还有focus和target伪类。以及结构化伪类。<del>first-child,nth-child什么的太麻烦。</del>甚至我们还可以用伪元素，两个冒号。first-letter用来做首字下沉，before,after用来处理动态内容。</li>
<li>css中有个特指度决定了应用css的优先级。有个ice规则可以看一下。 </li>
<li>盒模型以前说得很多这次就不说啦。只是我经常忘掉“固定定位”（fixed）是不随着屏幕滚动而变化的定位方式。</li>
<li>围住浮动元素的三种方法包括：
<ul>
<li> 为父元素添加overflow:hidden</li>
<li> 同时浮动父元素 </li>
<li> 添加一个非浮动的clear元素 </li>
</ul>
</li>
<li>建议把<code> * {margin:0;padding:0}</code>设置为所有css的第一个规则。</li>
<li>对于相当长的超链接，我们或许需要应用word-wrap:break-word来避免它们超过它们的父容器。</li>
<li>IE条件注释[if lte IE 8]和polyfill可以使得很多旧版本浏览器变得厉害。polyfill脚本参见<a href="http://github.com/modernizr/modernizer/wiki/html5-cross-browser-polyfills">腻子脚本</a>。其中最重要的，可能是html5shiv, selectivizr, ie9, css9pie, respond, -prefix-free, borderboxmodel...</li>
</ul>


<h2>css3特性和响应式设计</h2>
<ul>
<li>背景渐变。linear-gradient,-vsp-radial-gradient。vsp是厂商前缀，包括moz, webkit, ms, o,几大浏览器
<li>------华丽的分割线--------</li>
<li>响应式设计的三个重要方面：媒体查询，流式布局，弹性图片。媒体查询可以应用到link标记中，例如，<code>link type="text/css" media="screen and (max-width:568px)"</code>。或者，使用@media里面嵌套css规则。流式布局就是把所有宽度都用百分比来实现，或者使用em单位。</li>
</ul>



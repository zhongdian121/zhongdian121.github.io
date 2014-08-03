---
layout: post
keywords: blog
description: blog
title: "BigSolution工程技术备忘"
categories: [项目实战]
tags: [Archive]
group: archive
icon: file-o
---



BigSolution工程是一个大工程，从后端到移动端，基本上时兴的技术都会用到。它大概是在7月初开始需求分析，7月21日回家之后开始着手做，预计应该在8月20日做完，时间确实紧到没话说。

<h3>需求分析</h3>


<h3>服务器端</h3>
<h4>阿里云配置</h4>
由于赶上了好时代，阿里云的云主机（ECS）和关系型数据库(RDS)都在促销，这使得我能够极地成本地运营前面六个月，这大大地解决了资金链等问题。阿里云的RDS关系数据库服务要区分内外网模式，并且同时只能一种模式，测试期间，我使用外网接入，本地主机测试。正式运营期间，我准备使用内网接入，云主机测试。不过这样导致了测试期间会有RDS额外的公网流量费用。

<h4>操作系统</h4>
作为一个非常激进的童鞋，我一下子就选择了windows server 2012 x64的操作系统，安装了iis，不知道现在能不能正确使用webAPI访问了。当然选择2012版，其自带的.net 4.5更给我提供了现在所有能够用到资源的应用环境。

<h4>mySQL5.5</h4>
RDS上我选择了mySQL5.5，系统反正白送，5G空间不用也不好，用来存储用户的基本资料还是很可以。但是结果一用发现开发难度上加大了好多，7月28号开始就被这个整的无心恋战。最初看了点linq，后来发现linq to sql对mysql支持并不原生，想要使用还非得借助alinq或者ef，一步步觉得心塞。
```c#
			string connStr = "server=myaibig1.mysql.rds.aliyuncs.com;user=testor;database=testdata;port=3306;password=bugaosuni;";
            MySqlConnection conn = new MySqlConnection(connStr);
            try
            {
                Console.WriteLine("Connecting to MySQL...");
                conn.Open();
                // Perform database operations
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.ToString());
            }
            conn.Close();
            Console.WriteLine("Done.");
```
索性后来尝试了一下连接数据库，用传统的方式访问云数据库没什么区别，顿时觉得前途开朗了。这样下去，只要照着教程，CRUD一步步来就是了！<del>等等，今天已经八月三号了。。。。</del>

<h3>iOS客户端</h3>

<h3>Android客户端</h3>
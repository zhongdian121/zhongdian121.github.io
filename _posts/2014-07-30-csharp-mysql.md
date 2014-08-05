---
layout: post
keywords: blog
description: blog
title: "c#使用connector访问mysql"
categories: [后端.net]
tags: [Archive]
group: archive
icon: file-o
---



BigSolution工程从暑假开始进行到现在，还几乎没有产生最终代码。前几天玩的有点疯了，心收不太回来。今天也是急了，差不多把阿里云的壳子弄好了，RDS准备就绪，心想着学会Linq to mySQL就可以上路了。可谁知道这linq其实还是挺复杂的，而且对mysql的支持并不是原生的，必须借助alinq或者ef才能使用，文档都懒得看嫌太复杂，还是就借助官方的文档一步步来吧。
官方在线文档：http://dev.mysql.com/doc/connector-net/en/index.html

####连接
```
			string connStr = "server=myaibig1.mysql.rds.aliyuncs.com;"
				+"user=testor;database=testdata;port=3306;password=bugaosuni;";
			//This is the connect string to my RDS. Of course the password is a joke.
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
我还以为连接云数据库会费点周章，结果基本上什么都没有做就ok了。看来阿里云的易用性还是好顶赞。

####基本操作
跟以前用的sql server一样，MySqlCommand Object也是主要有三种方法：

• ExecuteReader - used to query the database. Results are usually returned in a MySqlDataReader object, created by ExecuteReader. 
• ExecuteNonQuery - used to insert and delete data. 
• ExecuteScalar - used to return a single value. 

读取数据
```
 			string sql = "SELECT Name, HeadOfState FROM Country WHERE Continent='Oceania'";
            MySqlCommand cmd = new MySqlCommand(sql, conn);
            MySqlDataReader rdr = cmd.ExecuteReader();

            while (rdr.Read())
            {
                Console.WriteLine(rdr[0]+" -- "+rdr[1]);
            }
            rdr.Close();
```

插入数据（或者创建表什么的）
```
 			string sql = "INSERT INTO Country (Name, HeadOfState, Continent)"
 				+" VALUES ('Disneyland','Mickey Mouse', 'North America')";
            MySqlCommand cmd = new MySqlCommand(sql, conn);
            cmd.ExecuteNonQuery();
```

统计（没找到好名字，相当于linq里的立即执行类）
```
 			string sql = "SELECT COUNT(*) FROM Country";
            MySqlCommand cmd = new MySqlCommand(sql, conn);
            object result = cmd.ExecuteScalar();
            if (result != null)
            {
                int r = Convert.ToInt32(result);
                Console.WriteLine("Number of countries in the World database is: " + r);
            }
```

总而言之，基本的操作，都是靠SQL。。。。<del>一到这里我又想因为以前自己不认真学习而撞墙了。</del>

####非实时连接
接下来就是我一开始就学，但是一直觉得没什么用的dataset和dataadapter部分了。不出意外地我依旧觉得这个，在bigSolution里面其实没什么作用（按照目前的数据库设计，mySQL仅仅维护一张用户信息表)，把官网的地址贴出来备查就是了。
http://dev.mysql.com/doc/connector-net/en/connector-net-tutorials-data-adapter.html

####简单封装
因为整个差不多是使用的webAPI特有的MVC架构，所以我想把数据访问放在底层便于上面操作。最初想使用泛型来完成，但是发现我自己太naive，后来采用了反射的方法封装了底层。
```
    // 此类型根据所给的sql返回一个结果给指定的Model。本想使用where子句限定传入的泛型应该属于Model类，但苦于各model不是派生自同一类，所以建了一个rootmodel空类型，不知道有没有坏处。
    public class getOneResultBySQL<T> where T:WebAPI.Models.RootModel
    {
        // 返回一个结果的通常查询。必须要保证数据库名称和Model成员名一致，尚未对错误机制进行开发。
        public static T getCommonOneResult(T resultModel,string[] para,string sql) 
        {
            MySqlConnection conn = new MySqlConnection(Universal.connStr);
            try
            {
                conn.Open();
                MySqlCommand cmd = new MySqlCommand(sql, conn);
                MySqlDataReader rdr = cmd.ExecuteReader();

                //因为此处只返回一个查询结果
                if (rdr.Read() != false)
                {
                    Type type = resultModel.GetType();
                    for (int i = 0; i < para.Length; i++)
                    {
                        PropertyInfo info = type.GetProperty(para[i]);
                        info.SetValue(resultModel, rdr[para[i]].ToString(), null);
                    }
                }
                rdr.Close();
                conn.Close();
                
                return resultModel;
            }
            catch (Exception ex)
            {
                conn.Close();
                return resultModel;
            }
        }
    }
```
在调用时，需要给出Model实例、Model的成员参数名数组和SQL语句作为参数。不过应当注意，目前来说，后台程序是不会对参数名列表做检验的，而且导致的错误也比较难以理解，所以在编程时自身要注意这里不要犯错。anyway，这种封装方式确实大大提高了代码重用性。百度了一下，这个也不会导致几何级数的效率降低，基本上可以接受。
```
            UserInfoModel userInfo = new UserInfoModel();
            string sql = "SELECT * FROM USERS WHERE uid=" + id.ToString();
            string[] paras = new string[] { "username", "password","email","birthday","uid","discription" };
            userInfo = getOneResultBySQL<UserInfoModel>.getCommonOneResult(userInfo, paras, sql);
            if (userInfo.username != null)
                return Ok(userInfo);
            else
                return NotFound();
```
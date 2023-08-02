## Springboot通过JDBC连接SQL Server数据库
由于项目需要，写了一个简单的通过JDBC连接SQL Server数据库（server v2019）的案例，其中加入了计算数据库连接并执行一条取数据的SQL语言所需的时间。如果有需要欢迎参考。
### 1. pom.xml文件引入驱动
[SQL Server 驱动的Maven仓库坐标](https://mvnrepository.com/artifact/com.microsoft.sqlserver/mssql-jdbc)
[SQL Severe 官网介绍](https://learn.microsoft.com/zh-cn/sql/connect/jdbc/working-with-a-connection?view=sql-server-ver16)

数据库驱动映入方式，在pom.xml文件中添加如下dependency
```bash
		<dependency>
			<groupId>com.microsoft.sqlserver</groupId>
			<artifactId>mssql-jdbc</artifactId>
			<version>9.2.0.jre8</version>
		</dependency>
```
### 2. 连接代码
思路是通过一个Rest接口"/db"触发数据库的连接操作，其中返回值为连接数据库以及执行SQL语句的时间。
```bash
package com.example.demo.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;
import java.sql.*;

@RestController
public class TestCon {

    @GetMapping("/db")
    public String dbConnect() throws ClassNotFoundException {
        String url="jdbc:sqlserver://;serverName=localhost;databaseName=master";
        String user="sa";
        String pwd="SA@12345";
        String conTime = "";

        Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");

        try {
            // 1.获取开始时间
            long startTime = System.currentTimeMillis();

            // 2. 建立数据库连接
            Connection connection = DriverManager.getConnection(url, user, pwd);

            System.out.println("数据库连接成功");

            // 3.获取传输器
            Statement st = connection.createStatement();

            // 4.通过传输器发送SQL到服务器执行并且返回执行结果
            String sql = "SELECT Column1, Name FROM yiqi.dbo.NewTable;";

            ResultSet rs = st.executeQuery(sql);
            // 5.数据处理
            while (rs.next()) {
                int id = rs.getInt("Column1");
                String name = rs.getString("Name");
                System.out.println(id + ":" + name);
            }

            // 6. 获取结束时间，并计算连接数据库，执行SQL语句时间
            long endTime = System.currentTimeMillis(); //获取结束时间
            conTime = "程序运行时间：" + (endTime - startTime) + "ms";
            System.out.println(conTime); //输出程序运行时间

        } catch (Exception e) {
            throw new RuntimeException(e);
        }
        return conTime;
    }
}
```

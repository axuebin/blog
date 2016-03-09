---
layout: post
title:  "servlet连接mysql"
date:   2016-03-9 09:43:54
categories: Java
---

* content
{:toc}

最近帮导师完成的一个项目是在做数据可视化，所以就需要用到servlet连接mysql读取数据。

## 连接数据库

首先我们需要建立数据库的连接。

```java
public class DBManager {
    //使用tomcat配置的数据库连接池来获取连接
    static public Connection get_connection()
    {
        Connection conn = null;
        try {      
            //初始化查找命名空间
            Context ctx = new InitialContext();  
            //参数java:comp/jdbc/learning_db为数据源和JNDI绑定的名字
            DataSource ds = (DataSource)ctx.lookup("java:comp/env/jdbc/dataminningdb"); 
            conn = ds.getConnection();
        } catch (Exception e) {
            //System.out.println(e);
            e.printStackTrace();
        }
        return conn;
    }
}
```

连接完数据库之后我们需要读取数据库中的数据。

```java
Connection con = null; Statement statement = null; ResultSet rs = null;
    try {
        con = DBManager.get_connection();
        String sql = String.format("select * from %s", table_name);
        statement = con.createStatement();
        rs = statement.executeQuery(sql);
        while(rs.next()) {
        }
    }catch(Exception e) { }
    finally {
        try { if(rs != null) rs.close(); } catch(Exception e) {}
        try { if(statement != null) statement.close(); } catch(Exception e) {}
        try { if(con != null) con.close(); } catch(Exception e){}
    }
```

## 写servlet

我们都知道servlet中其实就是对doGet()/doPost()方法进行重写，实现所需要的功能。

```java
public class PopulationQuery extends HttpServlet {
	 protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        response.setContentType("application/json; charset=utf-8");
        try {
            }
        }catch(Exception e) {}
    }
}
```
## 配置context.xml

需要在这个文件中配置有关数据库的一些参数。

```xml
name="jdbc/dataminningdb"
username="xb"
password=""
driverClassName="com.mysql.jdbc.Driver"
validationQuery='select 1'
url="jdbc:mysql://localhost:3306/dataminning"/>
```

## 配置web.xml

在这个文件中配置servlet

```xml
<servlet>
        <servlet-name>PopulationQuery</servlet-name>
        <servlet-class>dataminning.PopulationQuery</servlet-class>
</servlet>
<servlet-mapping>
        <servlet-name>PopulationQuery</servlet-name>
        <url-pattern>/PopulationQuery</url-pattern>
</servlet-mapping>
```

这是配置一个名为PopulationQuery的servlet，指向dataminning.PopulationQuery这个class，就会执行这个文件中的doGet/doPost方法。



# jdbc(Java DataBase Connectivity Java程序访问数据库的标准接口)

![jdbc.png](jdbc.png)

使用Java程序访问数据库时，Java代码并不是直接通过TCP连接去访问数据库，而是通过JDBC接口来访问，而JDBC接口则通过JDBC驱动来实现真正对数据库的访问.

实际上，一个MySQL的JDBC的驱动就是一个jar包，它本身也是纯Java编写的。我们自己编写的代码只需要引用Java标准库提供的java.sql包下面的相关接口，由此再间接地通过MySQL驱动的jar包通过网络访问MySQL服务器，
所有复杂的网络通讯都被封装到JDBC驱动中，因此，Java程序本身只需要引入一个MySQL驱动的jar包就可以正常访问MySQL服务器





## Mybatis

MyBatis 是一款优秀的持久层框架/半自动的ORM，它支持自定义 SQL、存储过程以及高级映射。MyBatis 免除了几乎所有的 JDBC 代码以及设置参数和获取结果集的工作。MyBatis 可以通过简单的 XML 或注解来配置和映射原始类型、接口和 Java POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录


### 优点


1、与JDBC相比，减少了50%的代码量


2、 最简单的持久化框架，简单易学


3、SQL代码从程序代码中彻底分离出来，可以重用


4、提供XML标签，支持编写动态SQL


5、提供映射标签，支持对象与数据库的ORM字段关系映射


### 缺点
1、SQL语句编写工作量大，熟练度要高

2、数据库移植性比较差，如果需要切换数据库的话，SQL语句会有很大的差异

## 参考

- https://mybatis.org/mybatis-3/

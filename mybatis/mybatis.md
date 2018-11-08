## Mybatis总结

### 基本概念
持久层框架，支持定制SQL,存储过程以及高级映射。封装了JDBC代码，封装参数及获取数据集。使用简单的XML或注解来配置和映射原生信息，将接口和Java中的对象映射成数据库中的记录。
http://www.mybatis.org/mybatis-3/zh/configuration.html

### 配置

- mybatis.type-aliases-package:别名所在包
- mybatis.mapper-locations:mapper文件所在文件夹


### 动态sql
- If:  <if test=”title != null” > And title like #{title}</if> 如果传入了title，那么进行模糊查询并返回BLOG结果。 否则返回上面要求的结果。  
- Choose，when, otherwise:choose和switch类似。
- SqlSession:执行持久化操作，类似于JDBC中的Connection.应用程序与持久层之间执行交互操作的一个单线程对象。底层封装了JDBC连接，可以用SqlSession实例来直接执行被映射的SQL语句。

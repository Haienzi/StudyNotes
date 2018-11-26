## Mybatis总结

### 基本概念
ORM （Object Relational GetMapping），对象关系映射。   
使数据库中的关系型数据映射为java中的对象。       
持久层框架，支持定制SQL,存储过程以及高级映射。封装了JDBC代码，封装参数及获取数据集。使用简单的XML或注解来配置和映射原生信息，将接口和Java中的对象映射成数据库中的记录。  
http://www.mybatis.org/mybatis-3/zh/configuration.html


### 对比
- Spring Data JPA:

### 配置

- mybatis.type-aliases-package:别名所在包

- mybatis.mapper-locations:mapper文件所在文件夹

### xml映射
- #{} 会导致Mybatis创建PreparedStatement参数并安全的设置参数。

- ${} 直接在sql语句中插入一个不转义的字符串

- resultType

- resultMap  
  - id & result：
   id和result都将一个列的值映射到一个简单数据类型的属性或者字段，区别：id表示的结果是对象的标识属性，这会在比较对象实例的时候用到。可以提高整体的性能，尤其是缓存和嵌套结果映射的时候。  

- <![CDATA[]]>和转移字符(xml解析器会忽略解析，所以更快)    
  被<![CDATA[]]>这个标记所包含的内容将表示为纯文本，比如<![CDATA[<]]>表示的是<


### 动态sql
- If:  <if test=”title != null” > And title like #{title}</if> 如果传入了title，那么进行模糊查询并返回BLOG结果。 否则返回上面要求的结果。  可选的根据条件查找文本的功能。

- where  
  where元素只会在至少有一个子元素的条件返回SQL子句的情况下才去插入where子句，若语句的开头为or或者and，where元素也会将它们去除。

- 如果where子句没有正常发挥作用，我们可以通过自定义trim元素，来定制where元素的功能。  
```
<trim prefix="WHERE" prefixOverrides="AND |OR">
...
</trim>
```

- set:动态包含需要更新的列舍去其它的  

  ```
  <update id="updateAuthorIfNecessary">
    update Author
      <set>
        <if test="username != null">username=#{username},</if>
        <if test="password != null">password=#{password},</if>
        <if test="email != null">email=#{email},</if>
        <if test="bio != null">bio=#{bio}</if>
      </set>
    where id=#{id}
  </update>

  ```

- Choose，when, otherwise:choose和switch类似。

- SqlSession:执行持久化操作，类似于JDBC中的Connection.应用程序与持久层之间执行交互操作的一个单线程对象。底层封装了JDBC连接，可以用SqlSession实例来直接执行被映射的SQL语句。


### 分页插件PageHelper的使用

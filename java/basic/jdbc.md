#### 数据库操作
https://www.cnblogs.com/chinafine/articles/1847205.html        



- 数据库表的int类型的字段映射到实体类中要使用Integer类型而不是int类型？  
如果返回字段值为null,int类型会报错，Integer不会报错，因为int类型声明的是变量，而null是对象所以会报错。Integer是包装类，包装类符合对象的特征并提供了一些必要的属性和方法。    
int类型的默认值是0，integer类型的默认值为null.


- DatabaseMetaData  
  有关整个数据库的信息：表名、表的索引、数据库产品的名称和版本、数据库支持的操作。

- ResultSet    
   关于某个表的信息或一个查询的结果。您必须逐行访问数据行，但是您可以任何顺序访问列

- ResultSetMetaData   
   有关 ResultSet 中列的名称和类型的信息。

  ```
如果将ResultSet的结果映射到HashMap中，要使用getColumnLabel，而不要用getColumnName，这样可提高程序的健壮性

 理由：

 getColumnLabel是field的SQL AS的值（Alias--别名）。
 比如：select
          a.name as name,
          a.description as description,
          b.description as relatedDescription
         from a,b where ...
 此时,getColumnName(3) == "description";而getColumnLabel(3) == "relatedDescription"。
 ```

- CLOB(Character Large Object)  
SQL中内置类型，将字符大对象存储为数据库表某一行中的一个列值。

- queryForObject(String sql，Object[] args,class<T> requiredType)
 ```
 JdbcTemplate jdbcTemplate = new JdbcTemplate();
 String sql = ”select count(*) from user”;  
 //queryForObject()方法中，如果需要返回的是int类型，就写Integer.class,需要返回long类型就写long.class.  
 int count = jdbcTemplate.queryForObject(sql,Interger.Class);
 ```

-

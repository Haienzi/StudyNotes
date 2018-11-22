## JAVA知识点

#### 泛型
1. Public < T > T success(){…}  
第一个<T>表明该方法时泛型方法  
第二个T表明该方法的返回值类型是泛型。


#### 概念
1. Java Bean：有默认构造方法，只有set,get方法的java类的对象。  
定义了一组规则，遵循此规则的平常的java对象。  
 - 实现Serializable接口。  
 - 提供无参数的构造函数  
 - 提供getter和setter方法访问它的属性。

#### 集合
1. HashMap
 - 根据键的hashCode值存取数据，键不允许重复，但是值允许重复。
 - 可以根据键直接获取它的值，具有很快的访问速.  
 - 最多允许一条记录的键为null,允许多条记录的值为null.    
 - 不支持线程同步，即任一时刻可以有多个线程同时写HashMap，会导致数据的不一致。  
 - Collections的synchronizedMap方法使HashMap具有同步的能力。  


2. LinkedHashMap  
内部通过一个双向链表使元素有序  
https://www.cnblogs.com/xiaoxi/p/6170590.html    


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
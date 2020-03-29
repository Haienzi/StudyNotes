## JAVA知识点

#### 泛型
1. Public < T > T success(){…}  
第一个<T>表明该方法是泛型方法  
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

3. CaseInsensitiveMap 不区分大小写的无序map
   "Name"和"name"会被视为相同的键key
4. LinkedCaseInsensitiveMap 不区分大小写的有序map


#### 注解

- `@PostConstruct`：javaEE5开始，修饰的方法会在服务器加载Servlet的时候运行，并且只会被
服务器调用一次，类似于Servlet的init()方法，会在构造函数之后，init()之前运行。

- `@PreDestroy`:javaEE5开始,修饰的方法会在服务器卸载Servlet的时候运行，并且只会被服务器
调用一次，类似于Servlet的destroy()方法。被@PreDestroy修饰的方法会在destroy()方法之后
运行，在Servlet被彻底卸载之前。

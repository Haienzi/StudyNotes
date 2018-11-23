## DataCenter


### AOP

https://www.cnblogs.com/liuruowang/p/5711563.html
- OOP:抽象，封装，继承，多态，建立一种对象的层次结构，它强调了一种完整事物的自上而下的关系。  
- AOP称为面向切面编程，用来解决一些系统层面上的问题    
将通用需求从不相关类之中分离出来，同时，能够使很多类共享一个行为，一旦行为发生变化，不必
修改很多类，只要修改这个行为就可以。
AOP技术则恰恰相反，它利用一种称为"横切"的技术，能够剖解开封装的对象内部，并将那些影响了多个类并且与具体业务无关的公共行为 封装成一个独立的模块（称
为切面）。更重要的是，它又能以巧夺天功的妙手将这些剖开的切面复原，不留痕迹的融入核心业务逻辑中。这样，对于日后横切功能的编辑和重用都能够带来极大
的方便。

（1）Aspect(切面)：通常是一个类，里面可以定义切入点和通知           
（2）JointPoint(连接点)：执行过程中明确的点，一般是方法的调用  
（3）Advice(通知)：在特定的切入点上执行的增强处理  
（4）PointCut(切入点)：带有通知的连接点  
（5）AOP代理：AOP框架创建的对象  

  ###### 使用说明
 - ` @Aspect` 说明是一个切面  
 - `@Before("execution()")` :定义前置通知，在execution指定的目标方法执行之前执行，在before方法内可以拿到目标方法的所有参数，进行方法的加强。  
 - ` @After("execution()")` :后置通知，在execution指定的目标方法执行之后执行，无论是否发生异常，不能访问到返回值
 - `@AfterRunning` 在方法成功执行返回结果后执行
 - `@AfterThrowing` 在方法抛出异常之后执行
 - `@Around` 环绕执行 前后都执行
 - `execution (*com.sample.web..*.*(..))    `  
  execution(modifiers-pattern? ret-type-pattern declaring-type-pattern? name-pattern(param-pattern)throws-pattern?)

 ```
 括号中各个pattern分别表示：

 修饰符匹配（modifier-pattern?）
 返回值匹配（ret-type-pattern）可以为*表示任何返回值,全路径的类名等
 类路径匹配（declaring-type-pattern?）
 方法名匹配（name-pattern）可以指定方法名 或者 *代表所有, set* 代表以set开头的所有方法
 参数匹配（(param-pattern)）可以指定具体的参数类型，多个参数间用“,”隔开，各个参数也可以用“*”来表示匹配任意类型的参数，如(String)表示匹配一个String参数的方法；(*,String) 表示匹配有两个参数的方法，第一个参数可以是任意类型，而第二个参数是String类型；可以用(..)表示零个或多个任意参数
 异常类型匹配（throws-pattern?）
 其中后面跟着“?”的是可选项

 (1). 第一个*：表示返回类型  
 (2). 包名：表示要拦截的包名，后面两个点表示当前包和当前包下的所有子包下  
 (3)第二个*：表示类名，* 号表示所有的类  
 (4)第三个*：表示所有的方法名  
 (5)(..):表示方法的参数，两个点表示任何参数
```

###### JDK动态代理和CGLIB动态代理的区别
- 简单来说
 - JDK动态代理只能对实现了接口的类或者继承的类生成代理，而  不能针对类
 - CGLIB是针对类实现代理，主要是对指定的类生成一个子类，覆盖其中的方法。
- 依据  
 - 当Bean实现接口时，Spring就会用JDK的动态代理  
 - 当Bean没有实现接口时，Spring使用CGlib是实现  
 - 可以强制使用CGlib    
`  @EnableAspectJAutoProxy(proxyTargetClass = true)`



### log4j



### 知识点

- hql: hibernate Query Langusge,更加丰富灵活，更为强大的查询能力。
接近SQL语句查询语法。实体查询语句。

 > HQL 查询包括以下步骤:
获取Hibernate Session对象。  
编写HQL语句  
以HQL语句作为参数，调用Session的createQuery方法创建查询对象。  
如果HQL语句包含参数，则调用Query的setXxx方法为参数赋值。  
调用Query对象的list()或uniqueResult()方法返回查询结果列表（持久化实体集）

- ServletContextListener接口：能监听ServletContext对象的生命周期，实际上就是监听Web应用的生命周期。当Servlet容器启动或者终止Web应用的时候，会触发ServletContext事件。  
 - `contextInitialized(ServletContextEvent sce) `
   当Servlet启动web应用启动时调用该方法。调用完成后，再对filter以及启动时需要被初始化的Servlet进行初始化。
 - `contextDestroyed(ServletContextEvent sce)`  
   当Servlet 容器终止Web 应用时调用该方法。在调用该方法之前，容器会先销毁所有的Servlet 和Filter 过滤器。
- map
https://blog.csdn.net/bestone0213/article/details/47904107
  - keySet:键的集合
  - entrySet:键值对的集合，容量大的时候可以通过这种方式遍历。
  ```
  /第三种：推荐，尤其是容量大时
  System.out.println("通过Map.entrySet遍历key和value");
  for (Map.Entry<String, String> entry : map.entrySet()) {
   System.out.println("key= " + entry.getKey() + " and value= " + entry.getValue());
  }
  ```

- `SAXReader`

- `SessionFactory`
负责初始化Hibernate,充当数据源的代理，并负责创建Session对象。可以得到Session实例，完成对象持久化操作，负责创建和关闭session对象。  
Session是Hibernate持久化操作的基础。  
```
Session session = SessionFactory.openSession();
```
session持久化方法：
增删改查
 - save(Object o):保存实体
 - flush()：将缓存中的数据持久化到数据库中，与数据库中的数据同步   
 - saveOrUpdate():保存或者更新，id不存在的时候使用save()否则使用update()

- Redis缓存
https://blog.csdn.net/tianzongnihao/article/details/54924924
 - 2.x sharedJedis 通过一致性hash来实现分布式缓存，通过一定的策略把不同的key分配到不同的redis server
 - 3.x 加入了集群功能
 - 关于jedis跟lettuce的区别：  
  Lettuce 和 Jedis 的定位都是Redis的client，所以他们当然可以直接连接redis server。  
  Jedis在实现上是直接连接的redis server，如果在多线程环境下是非线程安全的，这个时候只有使用连接池，为每个Jedis实例增加物理连接.  
  Lettuce的连接是基于Netty的，连接实例（StatefulRedisConnection）可以在多个线程间并发访问，应为StatefulRedisConnection是线程安全的，所以一个连接实例（StatefulRedisConnection）就可以满足多线程环境下的并发访问，当然这个也是可伸缩的设计，一个连接实例不够的情况也可以按需增加连接实例。

- 原子操作：这种操作一旦开始，就一直运行到结束，中间不会有任何的切换

- MQ服务




### 项目
- 数据库操作类
dao:
接口定义:IBaseDao
实现：BaseDao


问题：
1. core.listener.ServerListener.class中为什么要检查两次？
第一步检查函数，序列，表，视图等是否存在。都存在的情况下开启第二轮检查，获取数据。
2. 运行时浏览器总是出现401错误 中文乱码
shrio service配置为自己电脑的ip地址，端口号和tomcat的端口号保持一致。tomcat启动时路径配置为shrio service保持一致。
3. EMPI（Enterprise Master Patient index)  
 患者主索引：患者基本信息检索目录,主要用途是在一个复杂的医疗系统中，通过唯一的患者标识将多个医疗信息系统有效的关联在一起。。以实现各个系统之间的互联互通，保证对同一个患者，分布在不同系统中的个人信息采集的完整性和准确性。建立患者主索引是实现大型医院内部系统集成，医院集团内资源共享，以及建立居民健康档案实现区域医疗共享的必要条件。
4. AlarmPersonImpl ->dto.getSearch();
 dto.getSearch()?获取传输对象中的sql语句
save():首先判断数据库中是否存在该用户

5. CheckUtil作用？
   CloneUtil作用？

6. BaseController类中  
   pageDraw?  
   ResponseEntity?  
   ModelMap?
7. etlloader中：
com.example.exe-》Exe.java
jdbcTemplate



   -

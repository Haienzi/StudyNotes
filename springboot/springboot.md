
## Spring boot



### SpringBoot 从入门到实战

#### 第三章
1. 计划任务  
  @EnableScheduling    @Scheduled  
  cron表达式   fixDelay  fixRate（每隔指定毫秒运行任务）  

- 条件注解@Conditional:
   - 根据满足某一特定条件创建一个特定的bean.
   - 通过实现Condition接口，并重写其matches方法来构造判断条件。  

- 组合注解和元注解  
  元注解可以组合成组合注解

- @Enable*:   开启对 '  ' 的支持

- produces可定制返回的response的媒体类型和字符集。
@RequestMapping(produces="text/plain;charset=UTF-8")  
@RequestMapping(produces="application/json;charset=UTF-8")  




### Maven
软件项目管理工具，基于项目对象模型（Project Object Model,POM)
用来管理项目的依赖，编译，文档等信息。


### 区别
`Spring`:依赖注入框架  
`Spring MVC`：基于Servlet的一个MVC开发框架主要解决Web开发的问题，配置复杂xml，JavaConfig,servlet处理繁琐。  
Spring Boot 简化了配置流程，专注于为服务接口方面的开发和前端解耦。

### 注解
- `@ComponentScan` 告诉Spring从哪里可以找到bean,来定义那些包需要被扫描。用于扫描指定包下的类。  
 1. 如果你的其他包都在使用了@SpringBootApplication注解的main app所在的包及其下级包，则你什么都不用做，SpringBoot会自动帮你把其他包都扫描了
 2. 如果你有一些bean所在的包，不在main app的包及其下级包，那么你需要手动加上@ComponentScan注解并指定那个bean所在的包    

- `@Component`：表明当需要创建类的时候，这个类是一个候选类。将普通javaBean实例化到Spring中，创建对应类的实例。泛指各种组件。就是说当我们的类不属于各种归类的时候（不属于@Controller、@Services等的时候），我们就可以使用@Component来标注这个类

- `@Service`：业务层bean

- `@SpringBootApplication`

- `@RestController` 构造型注释 spring在处理传入的web请求时考虑。

- ` @EnableScheduling` 启用定时任务相比Sping mvc不需要配置扫描器

- ` @RequestMapping`：提供路由信息，负责URL到Controller中的具体函数的映射。

- `@GetMapping`相当于@RequestMapping（RequestMethod = Get）

- `@Controller`：用于定义控制器类，在spring项目中由控制器负责将用户发来的URL请求转发到对应的服务接口（service层），一般这个注解在类中，通常方法需要配合注解@RequestMapping。

- `@ApiOperation` Swagger2里的，用来构建API说明文档。@ApiOperation(value = “接口说明”, httpMethod = “接口请求方式”, response = “接口返回参数类型”, notes = “接口发布说明”；)

- `@RequestMapping(“/home”)`  
Value:处理方法对应的请求路径值。
Method:HTTP请求所使用的方法类型
将HTTP请求映射到控制器的处理方法上。比如本例：localhost:8080/home

- `@RequestMapping(value{“”,”/page”,”page*”,”view/*,**/msg”})`;
可以匹配如下URL:
•	localhost:8080/home
•	localhost:8080/home/
•	localhost:8080/home/page
•	localhost:8080/home/pageabc
•	localhost:8080/home/view/
•	localhost:8080/home/view/view

- `@RequestParam`注解配合@RequestMapping,可以将请求的参数同处理方法的参数绑定在一起。Value值指定了需要被映射到处理方法参数的请求参数

- `@ControllerAdvice:`一般用于处理系统error,拦截出错信息，返回报错提示界面，防止用户看到一堆出错信息。可以作用在所有注解了@RequestMapping的控制器方法上。

- `@ExceptionHandler`:用于全局处理控制器里的异常，value属性可以过滤拦截条件

- `@InitBinder`:用来设置WebDataBinder,用于自动绑定前台请求参数到Model中。

- ` @ModelAttribute`:本来作用是绑定键值对到Model中，此处让全局的”@RequestMapping”都能获得在此处设置的键值对。

- `@ResponseBody`:表示返回的结果直接写入HTTP的响应体中。一般在异步获取数据时使用，比如使用Ajax异步获取json数据。

- `@RequestBody`：作用在形参列表上，用于将前台发送过来固定格式的数据（xml或者json等）封装为对应的javaBean对象，封装时使用的对象时系统默认配置的HttpMessageConverter进行解析然后封装到形参上。

- `@PropertySource:` 将properties配置文件中的值存储到Spring的environment中，Environment接口提供方法读取配置文件中的值。参数是properties文件中定义的key值。
- ` @value` 与属性文件中的key值匹配。@Value注解可以用在字段和方法上。通常用于从属性配置文件中读取属性值，也可以设置默认值。
```
@value("${key:default")
private String var;
```
以上声明指导spring根据key去属性配置文件查找value，如果没找到，则使用default作为默认值。
- `@Transactional(readOnly=true)`:只读事务
从这一点设置的时间点开始到这个事务结束的过程中，其他事务所提交的数据该事务看不到。查询中不会出现别人再时间点a之后提交的数据。
- `@XmlAccessorType(XmlAccessorType.NONE)`
xml和java对象互相转化
-  @Repository,作用于持久层表明该类是用来执行数据库相关的操作，作为数据库的bean来使用，可以直接对数据库进行操作

- @PathVariable: 微博两个不同用户的个人主页对应两个不同的URL,对于这个用户则可以用变量来表示。
 - 定义url变量规则
   @RequestMapping("/users/{username}")
   {username}就是定义的变量部分
   注意：变量中不能包含URL的分隔符/
   @RequestMapping注解中用{}来表明变量部分。
  - 获取url变量
    ```
    @RequestMapping("/users/{username}")
   @ResponseBody
   public String userProfile(@PathVariable String username){
//        return String.format("user %s", username);
       return "user" + username;
   }
    ```
   在上述例子中，当@Controller处理HTTP请求时，userProfile的参数username会自动设置为URL中对应变量username（同名赋值）的值  
   也可以指定@PathVariable使用URL中的哪一个变量
   @PathVariable("username")

- @Bean 作用到方法上告诉spring 可以从这个方法中得到一个bean







### JAXB
https://blog.csdn.net/sd4015700/article/details/39474893
Java Architecture for XML Binding  
java对象和xml互相转换。
是一项可以根据XML Schema产生Java类的技术。该过程中，JAXB也提供了将XML实例文档反向生成Java对象树的方法，并能将Java对象树的内容重新写到XML实例文档。从另一方面来讲，JAXB提供了快速而简便的方法将XML模式绑定到Java表示，从而使得Java开发者在Java应用程序中能方便地结合XML数据和处理函数。

### 集成数据库连接池druid
#### 基本

建立数据库连接是耗时和耗费资源的行为，所以通过连接池预先同数据库建立一些连接，放在内存中，应用程序需要建立数据库连接时直接到连接池中申请一个就行，用完后再放回。
> https://blog.csdn.net/yanguo110/article/details/68944659

- 针对所有sql的监控，运行效率。
- 对于url的监控，请求时间，并发。
- 监控session

#### druid-spring-boot-starter

>https://blog.csdn.net/niugang0920/article/details/82703203

- jdbc配置
- 连接池配置
- 监控配置
- 配置多数据源
- 配置filter  

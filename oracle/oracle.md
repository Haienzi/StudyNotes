## Oracle使用总结


### 创建表时错误
- ORA_00955:名称已由现有对象使用  
 1. 查看是否存在重名的视图表，修改名称或者删除重复的对象  
 2. 如果没有重名的对象，执行下面的语句刷新共享池    
  `alter system flush shared_pool;`
- 列在此处不允许  
  使用insert语句时注意字符串类型使用单引号而不是双引号  
  `insert into SBD_USER values (001,'大西瓜',17,'男','王者')`

### 数据类型
- varchar对于汉字占两个字节，对于英文占一个字节，是标准sql里使用的，对空串不处理，存放固定长度的字节，最大长度是2000
- varchar2是oracle中独有的数据类型，对于汉字和英文都是占两个字节，将空串当作null来处理，存放可变长度字节，最大长度是4000

### 查询语句
- oracle中列名可以用as 来创建别名，表的别名则不需使用as，直接写即可。  
`SELECT SAL*12+NVL(CID,0)*2 "总奖金",STUNAME,CID FROM SBD_STUDENT ScholarShip;`
- nvl函数 （可以用来处理null值）  
 - 格式为：`nvl(string1,replace_with)`  
 - 功能：如果string1为null,则nvl函数返回replace_with的值，否则返回string1的值。
- distinct函数 去除重复的值  
`select distinct deptno, job from emp;`
- 使用（||）连接字符串  
`SELECT STUNAME || ' is in ' || CID from SBD_STUDENT;`  
![图片]https://github.com/Haienzi/StudyNotes/blob/master/image/oracle-connect.png
-
- order by 排序  
`select STUNAME from SBD_STUDENT order by STUNAME desc ;`
- 对多列数据排序 首先按照stuname进行升序排列，接着对stuname相同的部分按照降序排列  
`select STUNAME,BIRTHDAY from SBD_STUDENT order by STUNAME,BIRTHDAY desc ;`
- 用null值排序行  nulls first null值在前面 nulls last null值在后面  
`select SAL from SBD_STUDENT order by SAL NULLS FIRST;`  
`select SAL from SBD_STUDENT order by SAL NULLS last ;`
- group by用于对查询的结果分组统计，having用于限制分组统计结果
>注意：如果要分组的话，分组的字段一定要显示在查询中。  

 1. 分组函数只能出现在选择列表，having, order by子句中，不能出现在where中。
 2. group by -> having  -> order by
 3. 在选择列中如果有列、表达式和分组函数，那么这些列和表达式必须有一个出现在group by 子句中，否则就会出错。

- 多表查询  
  （1） 自连接 自连接是指在同一张表的连接查询。  
  （2） 子查询 子查询是指嵌入在其他sql语句中的select语句

- 多行子查询
  ```
  (1) 查询出部门10的所有工作(返回多行结果集)
	SELECT DISTINCT job FROM emp WHERE deptno = 10;  
(2) 显示
	SELECT * FROM emp WHERE job IN (SELECT DISTINCT job FROM emp WHERE deptno = 10);
	注意：不能用job=..，因为等号=是一对一的
  ```
- 合并查询： union（联合）/union all/intersect(交叉)/minus（减少）  
目的：为了合并多个select语句的效果  
  （1）`union` 该操作符用于取得两个结果集的并集。当使用该操作符的时候，会自动去掉结果集中重复的行。    
  注意：使用的时候前后两个查询字段数量，类型，顺序必须相同。字段名称可以不相同  
  > 场景：
  当两个select的结果集个别字段有差别时需要UNION 或UNION ALL 合并。  
  解决办法：
  某个结果集少字段可以用空值或固定值代替，使用别名达到列名一致要求。

  （2）`union all` 与union类似，但是不会取消重复行，而且不会排序。  
  （3）`intersect` 使用该操作符用于取得两个结果集的交集  
  （4）`minus` 使用该操作符用于取得两个结果集的差集,只显示存在第一个集合的数据而不存在第二个集合中的数据。
- 分页查询  
 (1) rownum：伪列Oracle首先进行查询获取到结果集之后在加上去的一个伪列，这个伪列对符合条件的结果添加一个从1开始的序列号。  
 rownum是动态的必须先有查询到的结果集，然后再给这个结果集加上一个列。



### 连接
- 内连接 只连接匹配的行
- 左外连接 包含左边表的全部行（不管右边的表中是否存在与他们匹配的行），以及右边表中全部匹配的行
- 右外连接 包含右边表的全部行（不管左边的表中是否存在与它们匹配的行）,以及左边表中全部行
- 全外连接 包含左右两个表的全部行，不管另外一边是否存在与它们匹配的行




### 函数
- `TRUNC()函数`：类似截取函数，按照指定的格式截取输入的数据。
    select to_char(sysdate,'yyyy-mm-dd hh24:mi:ss') from dual;
    'yyyy-mm-dd hh24:mi:ss'：2014-01-22  10：29：48
     Oracle中mm是月份，mi是分钟。  
  博客说明：
  https://www.cnblogs.com/linjiao/p/6394087.html
- `TO_CHAR`:把日期或者数字转换为字符串。
  `TO_DATE`:把字符串转换为数据库中的日期类型
  https://www.cnblogs.com/hllnj2008/p/5332962.html
- `Extract()`用于从date类型或者interval类型中截取到特定的部分
- Oracle常用函数
  https://www.cnblogs.com/lxl57610/p/7442130.html

- `数据库中的事务回滚`：发生错误之前的所有数据库操作都回滚，不保存。

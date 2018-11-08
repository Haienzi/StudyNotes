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

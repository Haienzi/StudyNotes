## ETL

### 概念
Extract - Transform - Load的缩写，用来描述将数据从来源端经过抽取（Extract),转换（Transform），加载（load)至目的端的过程。

### 依赖
- jdk1.8

- python2.6.X

- apache-maven-3.X


### cmd
win10 配置python path环境变量  
- 测试  
 - 进入dataX目录下的bin文件  
  `python datax.py ../job/job.json`

 - 如果出现乱码：  
  `CHCP 65001`

 - 查找模板  
   `python datax.py -r streamreader -w streamwriter`

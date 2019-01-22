## ETL

### 概念
Extract - Transform - Load的缩写，用来描述将数据从来源端经过抽取（Extract),清洗转换（Transform），加载（load)至目的端的过程目的是将企业中的分散、零乱、标准不统一的数据到一起，为企业的决策提供分析依据。

主要有两个任务：数据流任务 旧的打包运输到新的数据仓库，清洗任务

BI:商务智能
ODS:操作型数据存储

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

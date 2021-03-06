
#### 分布式

- 分布式计算：把需要进行大量计算的工程数据分割成小块，由多台计算机分别计算，在上传运算
结果后，将结果统一合并得出数据结论的科学。


#### Session的持久化
1. 为什么需要持久化？
> 客户端访问了某个能开启会话功能的资源，web服务器就会创建一个与该客户端对应的HttpSession  
对象，每个HttpSession对象都要占用一定的内存空间。如果在某一个时间段内访问站点的用户很多，  
web服务器内存中就会积攒大量的HttpSession对象，消耗大量的服务器内存，即使用户已经离开或  
关闭了浏览器，web服务器仍要保留与之对应的HttpSession对象，在他们超时之前，一直占用Web  
服务器内存资源。
web服务器通常将那些暂时不活动但未超时的HttpSession对象转移到文件系统或数据库中保存，服  
务器要使用他们时再将他们从文件系统或数据库中装载入内存，这种技术称为Session的持久化。  
将HttpSession对象保存到文件系统或数据库中，需要采用序列化的方式将HttpSession对象中的每  
个属性对象保存到文件系统或数据库中；将HttpSession对象从文件系统或数据库中装载如内存时，  
需要采用反序列化的方式，恢复HttpSession对象中的每个属性对象。所以存储在HttpSession对象  
中的每个属性对象必须实现Serializable接口 。

2. Session的持久化的作用：
  1.提高服务器内存的利用率，保证那些暂停活动的客户端在会话超时之前继续原来的会话。  
  2.在多台web服务器协同对外提供服务的集群系统中，使用Session的持久化技术，某台服务器可  
  以将其中发生改变的Session对象复制给其他服务器。保证了在某台服务器停止工作后可以由其他  
  服务器来接替它与客户端的会话。    
  3.在一个web应用程序重启时，服务器也会持久化该应用程序中所有HttpSession对象，保证客户  
  端的会话活动仍可以继续。  

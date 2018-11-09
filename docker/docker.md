## Docker学习笔记

### 基本操作
1. 下载一个docker镜像 <br>
   `docker pull centos`
2. 查看镜像<br>
  `docker  images centos`
- 创建容器<br>
`docker create <image-id>`
- 开启容器 创建进程隔离空间<br>
`docker start <container-id>`
- 创建并运行容器<br>
`docker run <image-id>`
- 列出所有运行的容器<br>
`docker ps `
- 列出所有容器（包含非运行状态的）<br>
`docker ps -a`
- 列出所有顶层镜像<br>
`docker images`
- 列出所有容器(所有的可读层)<br>
`docker images -a`
- 停止容器<br>
`docker stop <container-id>`
- 删除容器<br>
`docker rm <comtainer-id>`
- 删除镜像<br>
`docker rmi <image-id>`
- 创建镜像<br>
`docker build -t images-name .`
- 指定端口jar文件创建并运行容器<br>
`docker run -d -p 8082:8080 --name jarname images-name`
- 开启docker服务<br>
`systemctl restart docker.service`

### 环境搭建
1. 搜索镜像  
`docker search image-name`
- 下载镜像  
`docker pull image-name`
- 启动镜像  
> 容器是在镜像的基础上运行的，一旦容器启动了，我们就可以登录到容器中，安装自己所需的软件或者应用程序。

 用法：`docker run <相关参数> <镜像 ID> <初始命令>`

 ```
 1. docker run -i -t -v /usr/localhost/:/data/soft/ 196e0ce0c9fb /bin/bash
  -i：表示以“交互模式”运行容器
  -t：表示容器启动后会进入其命令行
  -v：表示需要将本地哪个目录挂载到容器中，格式：-v <宿主机目录>:<容器目录>
 ```
 初始命令表示一旦容器启动，需要运行的命令，此时使用“/bin/bash”，表示启动后直接进入bash shell。

 进入容器后，ctrl+d 或者exit命令， 退出容器


### 配置springboot项目的环境
- 拉取centos:6的镜像
`docker pull centos:6`
- 利用镜像启动一个容器  
`docker run -i -t centos:6 /bin/bash`
- 安装jdk1.8的所有文件  
`yum install java-1.8.0-openjdk* -y`
- 检查是否安装成功  
`java -version`
- 运行jar包命令   
`java -jar sbd-0.0.1.jar --server.port=80`
- 进入一个容器  
`docker attach contianer-name`或者
 `docker attach container-id`
- 从容器里面拷贝文件到宿主机(在宿主机执行命令)  
将容器里的test.js文件拷贝到宿主机opt目录下  
`docker cp container-name：/usr/test.js /opt`
- 从宿主机里面拷贝文件到容器(在宿主机执行命令)  
将宿主机里的test.js文件拷贝到容器opt目录下  
`docker cp  /opt container-name：/usr/test.js`
>注意：前提是目录已经存在 创建目录命令：mkdir dirname

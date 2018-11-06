### Docker学习笔记

#### 基本操作
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

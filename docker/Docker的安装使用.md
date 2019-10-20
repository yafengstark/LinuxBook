

容器



## 1.2 docker特性

**文件系统隔离：**每个进程容器运行在完全独立的根文件系统里。

**资源隔离：**可以使用cgroup为每个进程容器分配不同的系统资源，例如CPU和内存。

**网络隔离：**每个进程容器运行在自己的网络命名空间里，拥有自己的虚拟接口和IP地址。

**写时复制：**采用写时复制方式创建根文件系统，这让部署变得极其快捷，并且节省内存和硬盘空间。

**日志记录：**Docker将会收集和记录每个进程容器的标准流（stdout/stderr/stdin），用于实时检索或批量检索。

**变更管理：**容器文件系统的变更可以提交到新的映像中，并可重复使用以创建更多的容器。无需使用模板或手动配置。

**交互式Shell：**Docker可以分配一个虚拟终端并关联到任何容器的标准输入上，例如运行一个一次性交互shell。



Docker使用了一种叫AUFS的文件系统，这种文件系统可以让你一层一层地叠加修改你的文件，最底下的文件系统是只读的，如果需要修改文件，AUFS 会增加一个可写的层（Layer），这样有很多好处，例如不同的Container可以共享底层的只读文件系统（同一个Kernel），使得你可以跑N多 个Container而不至于你的硬盘被挤爆了！这个只读的层就是Image！而如你所看到的，一个可写的层就是Container。

那Image和Container的区别是什么？很简单，他们的区别仅仅是一个是只读的层，一个是可写的层，你可以使用docker commit 命令，将你的Container变成一个Image，也就是提交你所运行的Container的修改内容，变成一个新的只读的Image，这非常类似于git commit命令。 



## Docker的安装

### Mac下安装Docker

[MacOS Docker 安装  菜鸟教程](https://www.runoob.com/docker/macos-docker-install.html)



* 使用 Homebrew 安装

## 使用

### 查看版本

```shell
docker --version
```

### 镜像加速

* 切换为网易镜像

###  查看容器运行情况

```
docker ps 
```

### 查看已经下载的镜像

```
docker images |grep mysql
```

#### 进入容器终端

```
docker exec -it  2a7a85124400（ID号）  /bin/bash
```

docker exec -it  76fadc25821f  /bin/bash



### 搜索可用镜像

docker search postgis



### 创建容器并运行



```shell
docker run --name postgis -e POSTGRES_PASSWORD=hellopg -d mdillon/postgis
```

### 启动和关闭容器

启动命令：

```
$ sudo docker start pwc-mysql   //通过指定容器名字
$ sudo docker start 73f8811f669e  //通过指定容器ID
```

关闭命令：

```
$ sudo docker stop pwc-mysql   //通过指定容器名字
$ sudo docker stop 73f8811f669e  //通过指定容器ID
```











## 安装软件



参考：

- [[Docker搭建MySQL服务](https://www.cnblogs.com/pwc1996/p/5425234.html)](https://www.cnblogs.com/pwc1996/p/5425234.html)



### mysql

#### 拉取镜像

```shell
docker search mysql
```

#### 使用镜像



* 运行容器1

```shell
docker run -p 3306:3306 --name mymysql -v $PWD/conf:/etc/mysql/conf.d -v $PWD/logs:/logs -v $PWD/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.6
```



命令说明：

- **-p 3306:3306**：将容器的 3306 端口映射到主机的 3306 端口。
- **-v $PWD/conf:/etc/mysql/conf.d**：将主机当前目录下的 conf/my.cnf 挂载到容器的 /etc/mysql/my.cnf。
- **-v $PWD/logs:/logs**：将主机当前目录下的 logs 目录挂载到容器的 /logs。
- **-v $PWD/data:/var/lib/mysql** ：将主机当前目录下的data目录挂载到容器的 /var/lib/mysql 。
- **-e MYSQL_ROOT_PASSWORD=123456：**初始化 root 用户的密码。



- 运行mysql2

sudo docker run --name pwc-mysql -e MYSQL_ROOT_PASSWORD=123456 -p 3306:3306 -d mysql:5.6



- –name：给新创建的容器命名，此处命名为`pwc-mysql`
- -e：配置信息，此处配置`mysql`的`root用户`的登陆密码
- -p：端口映射，此处映射`主机3306端口`到`容器pwc-mysql的3306端口`
- -d：成功启动容器后输出容器的完整ID，例如上图 `73f8811f669ee...`
- 最后一个`mysql`指的是`mysql镜像名字`



#### 进入mysql 终端

1. 进入docker终端
2. 

```
mysql -h 127.0.0.1 -u root -p 
```


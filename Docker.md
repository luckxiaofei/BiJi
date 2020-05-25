## Docker是什么？

Docker是开源的一个基于轻量级虚拟化技术的容器引擎项目。

####docker三大组件

- 镜像：


>  Docker运行容器前需要本地存在对应的镜像。
>
>  镜像可以用来创建Docker容器的。一个镜像可以包含一个完整的操作系统环境和用户需要的其它应用程序。在docker hub 里面有大量现成的镜像提供下载。docker的镜像是只可读的，一个镜像可以创建多个容器。


- 容器

> docker利用容器来开发、运行应用。
>   容器是镜像创建的实例。它可以被启动、开始、停止、删除。每个容器都是 相互隔离的、保证安全的平台。可写


- 仓库

>  仓库是集中存放镜像文件的场所。
>   每个 仓库中又包含了多个镜像，每个镜像有不同的标签（tag）。

-------

##Docker的应用场景

- Web 应用的自动化打包和发布。
- 自动化测试和持续集成、发布。
- 在服务型环境中部署和调整数据库或其他的后台应用。
- 从头编译或者扩展现有的OpenShift或Cloud Foundry平台来搭建自己的PaaS环境。

-------

## Docker 的优点

- **1、简化程序：**
  Docker 让开发者可以打包他们的应用以及依赖包到一个可移植的容器中，然后发布到任何流行的 Linux 机器上，便可以实现虚拟化。Docker改变了虚拟化的方式，使开发者可以直接将自己的成果放入Docker中进行管理。方便快捷已经是 Docker的最大优势，过去需要用数天乃至数周的	任务，在Docker容器的处理下，只需要数秒就能完成。
- **2、避免选择恐惧症：**
  如果你有选择恐惧症，还是资深患者。Docker 帮你	打包你的纠结！比如 Docker 镜像；Docker 镜像中包含了运行环境和配置，所以 Docker 可以简化部署多种应用实例工作。比如 Web 应用、后台应用、数据库应用、大数据应用比如 Hadoop 集群、消息队列等等都可以打包成一个镜像部署。
- **3、节省开支：**
  一方面，云计算时代到来，使开发者不必为了追求效果而配置高额的硬件，Docker 改变了高性能必然高价格的思维定势。Docker 与云的结合，让云空间得到更充分的利用。不仅解决了硬件管理的问题，也改变了虚拟化的方式。

-------

## docker安装

安装很简单，不做笔记了

-------

##Docker常用指令

```shell
查看本机镜像：Docker pull images

下载镜像：docker pull [imageName]

删除镜像：docker rmi [imageId]

运行：
前台运行：docker run [imageName]
后台运行：docker run -d [imageName]
后台运行，把docker的80端口映射到本地8080端口：docker run  -d  -p 8080：80/-P  [imageName]

停掉容器：docker stop [imageId]

查看正在运行的容器： docker ps

查看所有容器：docker ps -a

删除容器：docker rm [containerID]

进入容器：docker exec -it  name/ID bash

指令提示：--help
```
![image-20180902141014565](https://ws4.sinaimg.cn/large/006tNbRwgy1fuv5zll0c8j30kn0aigq5.jpg)

> host：和主机共享一个
>
> bridge：建立一个独立的端口和ip（默认）
>
> none：不建立（啥都不干）
>
> ```
> docker run -it --net=host [imageName]
> ```

####创建自己的镜像

  ```
vi dockerfile 
  ```

##### dockerfile语法

>https://www.cnblogs.com/dazhoushuoceshi/p/7066041.html

```sh
docker build -t [imagesName]:[tag]
```

------

## 删除镜像

学习docker的时候，制作、下载了很多镜像，后面想删掉无用的镜像，但是总是不能成功删除，在此做个笔记！

#####先删容器，再删镜像

```
查看所有容器：docker ps -a
删除容器：docker rm [ID]
查看所有镜像：docker images
删除镜像：docker rmi [ID]
```

##### id值一样，指定版本

两个镜像的id是一样的，可以通过版本号区分删除

```
停止所有容器：docker stop $(docker ps -a -q)
删除所有容器：docker rm $(docker ps -a -q)
```


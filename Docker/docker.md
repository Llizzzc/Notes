# Docker
>1. [M1配置Docker]("https://liuxiaocong.blog.csdn.net/article/details/122338153" "docker")
>2. [尚硅谷](https://www.bilibili.com/video/BV1gr4y1U7CY?p=16 "docker")

## 一、镜像命令
+ `docker info`	// 查看docker信息
+ `docker Command --help`	// 查看命令帮助
+ `docker images (-a, -q)`	// 显示镜像，-a显示所有，-q只显示id
+ `docker search Image (--limit=n)`	// 搜索镜像，--limit显示前n个
+ `docker pull Image(:Tag)`	// 下载镜像，可指定版本
+ `docker rmi (-f) Image($(docker images -aq))`	// 删除镜像，-f强制删除，可以一次删完，可通过id删除
+ `docker system df`	// 显示镜像，容器，数据卷所占空间

## 二、容器命令
有镜像才能创建容器
+ `docker run (--name="Name" -d -it -p -P) Image`	// 启动镜像，--name指定容器名字，-d后台运行，-it交互方式运行，要指定shell(/bin/bash)，exit退出并停止容器，ctrl+p+q只退出，-p指定端口，-P随机分配
+ `docker ps (-a -q -n=n -l)`	// 列出当前正在运行的容器，-a包含历史运行，-q只显示编号，-n显示最近创建的n个容器，-l显示最近创建容器
+ `docker rm (-f) Container($docker ps -aq)`	// 删除容器，-f强制，可一次删完，可通过id删除
+ `docker start Container`	// 启动容器
+ `docker restart Container`	// 重启容器
+ `docker stop Container`	// 停止容器
+ `docker kill Container`	// 强制停止容器
+ `docker logs Container`	// 查看容器日志
+ `docker top Container`	// 查看容器内运行的进程
+ `docker inspect Container`	// 查看容器内部细节
+ `docker exec -it Container /bin/bash`	// 重新交互进入容器，exit不会停止容器
+ `docker attach Container`	// 重新进入容器，exit会退出
+ `docker cp Contain:Source Destination`	// 拷贝容器内文件到目的主机
+ `docker export Container > Name.tar`	// 把容器内容打包为tar包
+ `cat Name.tar | docker import - ImageUser/Image:Tag`	// 恢复镜像
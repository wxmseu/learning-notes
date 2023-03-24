# docker

### docker镜像命令

```
docker images  列出所有本地的镜像
docker search 镜像名   搜索镜像
docker pull 镜像名 [:TAG]
docker system df 查看所占空间
docker rmi -f 镜像名/image id 删除镜像
attach      Attach local standard input, output, and error streams to a running container
  build       Build an image from a Dockerfile
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container's filesystem
  events      Get real time events from the server
  exec        Run a command in a running container
  export      Export a container's filesystem as a tar archive
  history     Show the history of an image
  images      List images
  import      Import the contents from a tarball to create a filesystem image
  info        Display system-wide information
  inspect     Return low-level information on Docker objects
  kill        Kill one or more running containers
  load        Load an image from a tar archive or STDIN
  login       Log in to a Docker registry
  logout      Log out from a Docker registry
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  ps          List containers
  pull        Pull an image or a repository from a registry
  push        Push an image or a repository to a registry
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  run         Run a command in a new container
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  search      Search the Docker Hub for images
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  version     Show the Docker version information
  wait        Block until one or more containers stop, then print their exit codes

```

面试题：docker虚悬镜像是什么：

```
仓库名、标签都是<nono>的镜像，俗称虚悬镜像dangling image
```

### docker容器命令

**新建+启动容器**

```
docker run [options] image  [command] [arg...]
option说明：有些是一个减号，有些是两个减号
--name='容器新名字'	为容器指定一个名称
-d：后台运行容器并返回容器id，也即启动守护式容器（后台启动）
-i：以交互模式运行容器，通常与-t同时使用
-t：为容器重新分配一个伪输入终端，通常与-i同时使用
也即 启动交互式容器（前端有伪终端，等待交互）

-P:随机终端映射，大写P
-p：指定端口映射，小写p
```

```
# 启动ubuntu
sudo docker run -it --name=myu1 ubuntu [/bin/bash]
# 退出ubuntu
exit;
```

**列出当前所有正在运行的容器**

```
docker ps [options]
-a:列出当前所有正在运行的容器+历史上运行过的
-l：显示最近创建的容器
-n:显示最近n个创建的容器
-q：静默模式，只显示容器编号
```

**退出容器**

```
exit     run进去容器，exit退出，容器停止
ctrl+p+q  run进去容器，ctrl+p+q退出，容器不停止
```

**启动已经停止运行的容器**

```
docker start 容器id或者容器名
```

**重启容器**

```
docker restart 容器id或者容器名
```

**停止容器**

```
docker stop 容器id或者容器名
```

**强制停止容器**

```
docker kill 容器id或者容器名
```

**删除已停止的容器**

```
docker rm 容器id
```



**有镜像才能创建容器，这是根本前提（下载一个redis6.0.8镜像演示）**

- 启动守护式容器（后台服务器）

```
docker run -d redis:6.0.8
```

- 查看docker运行容器日志

```
docker logs 容器id
docker轻量级可视化工具portainer
```

- 查看容器内运行的进行

```
docker top 容器id
```

- 查看容器内部细节

```
docker inspect 容器id
```

- 进入正在运行的容器并以命令行交互

```
docker exec -it 容器id bashShell
docker attach 容器id
两者区别：
attach直接进入容器启动命令的终端，不会启动新的进程，用exit退出会导致容器的停止
exec是在容器中打开新的终端，并且可以启动新的进程，用exit退出，不会导致容器的停止
```

- 从容器内拷贝文件到主机上

```
docker cp 容器id:容器内路径 目的主机路径
```

- 导入导出容器

```
exprot 导出容器的内容留作为一个tar归档文件[对应import命令]
import 从tar包中的内容创建一个新的文件系统再导入为镜像[对应export]

docker export 容器id>文件名.tar
cat 文件名.tar | docker import - 镜像用户/镜像名：镜像版本号
```

### docker镜像

**镜像**：是一种轻量级、可执行的独立软件包，它包含运行某个软件所需的所有内容，我们把应用程序和配置依赖打包好形成一个可交付的运行环境（包含代码、运行时需要的库、环境变量和配置文件等），这个打包好的运行环境就是image镜像文件。

镜像是分层的

unionFS（联合文件系统，union file system）

```
镜像分层最大的一个好处就是共享资源，方便复制迁移，就是为了复用。
比如说有多人镜像都从相同的 base 镜像构建而来，那么 Docker Host 只需在磁盘上保存一份 base镜像，同时内存中也只需加载一份 base 镜像，就可以为所有容器服务了。而且镜像的每一层都可以被共享。
```

重点理解：

```
Docker镜像层都是只读的，容器层是可写的。
当容器启动时，一个新的可写层被加载到镜像的顶部。这一层通常被称作“容器层”，“容器层”之下的都叫“镜像层”
```

提交副本

```
docker commit -m='提交的信息描述' -a='作者' 容器id 要创建的目标镜像名[:标签名]
```

创建一个添加vim的ubuntu到阿里云的docker registry

```
1. 再ubunt中安装vim
2. 提交副本
	sudo docker commit -m='add vim' -a='wxm' 35ff577bf928 wxmseu/myubuntu:1.0.1
3. 登录阿里云并push
	sudo docker login --username=wxmseu registry.cn-hangzhou.aliyuncs.com
	sudo docker tag 43f7af9460c8 registry.cn-hangzhou.aliyuncs.com/wxmseu/myubuntu:1.0.1
	sudo docker push registry.cn-hangzhou.aliyuncs.com/wxmseu/myubuntu:1.0.1
```



### 创建私有库

```
1. 下载镜像docker registry
	sudo docker pull registry
2. 运行私有库registry
	docker run -d -p 5000:5000 -v /zzyyuse/myregistry/:/tmp/registry --privileg=true registry 
默认情况下，仓库被创建再容器的/var/lib/registry 目录下，建议另行
3. curl验证私服库上有什么镜像
	curl -XGET http://127.0.0.1:5000/v2/_catalog
4.将新镜像修改符合私服规范的tag
	docker tag 镜像：tag host：port/repository“tag
	sudo docker tag wxmseu/myubuntu:1.0.2 127.0.0.1:5000/myubuntu:1.0.2
5. 修改配置文件使之支持http
	sudo vim /etc/docker/daemon.json
	{
  		"registry-mirrors": ["https://1yw00sea.mirror.aliyuncs.com"],
  		# 添加此行
 		 "insecure-registries": ["43.142.112.65:5000"]
	}
	# 重启
	sudo systemctl restart docker
6. push推送到私服库
	sudo docker push 127.0.0.1:5000/myubuntu:1.0.2
```

### docker容器数据卷

卷

```
卷就是目录或文件，存在于一个或多个容器中，由docker挂载到容器，
但不属于联合文件系统，因此能够绕过Union File System提供一些用于持续存储或共享数据的特性:
卷的设计目的就是数据的持久化，完全独立于容器的生存周期，因此Docker不会在容器删除时删除其挂载的数据卷
```

特点：

1. 数据卷可在容器之间共享或重用数据
2. 卷中的更改可以直接实时生效
3. 数据卷中的更改不会包含在镜像的更新中
4. 数据卷的生命周期一直持续到没有容器使用它为止

容器卷加入

```
docker run -d -p 5000:5000 -v 宿主机路径:容器内路径 --privileged=true 镜像名
docker挂载主机目录访问如果出现cannot open directory：permission denied，在挂载目录后加--privileged=true
```

查看容器是否挂载成功

```
docker inspect 容器id

"Mounts": [
            {
                "Type": "bind",
                "Source": "/home/ubuntu/test",
                "Destination": "/root",
                "Mode": "",
                "RW": true,
                "Propagation": "rprivate"
            }
        ],

```

容器和宿主机之间数据共享

1. docker修改，主机同步获得
2. 主机修改，docker同步获得
3. dockers容器stop，主机修改，docker容器重启数据同步

读写规则

```
docker run -d -v 宿主机路径:容器内路径:rw --privileged=true 镜像名
默认为读写 rw

docker run -d -v 宿主机路径:容器内路径:ro --privileged=true 镜像名
ro 只读read only
```

卷的继承和共享

```
docker run -it --privileged=true --volumes-from 父类 --name u2 ubuntu
主机和各继承的容器共享数据
```

### mysql主从复制

##### 主服务器

- 新建主服务器容器实例3306

```
sudo docker run -p 3306:3306 --name mysql-master -v /home/ubuntu/mysql/mysql-master/log:/var/log/mysql -v /home/ubuntu/mysql/mysql-master/data:/var/lib/mysql -v /home/ubuntu/mysql/mysql-master/conf:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD=root -d mysql
```

- 进入/home/ubuntu/mysql/mysql-master/conf 新建my.cnf

```
cd /home/ubuntu/mysql/mysql-master/conf
vim my.cnf

[mysqld]
## 设置server_id，同一局域网中需要唯一
server_id=101
## 指定不需要同步的数据库名称
binlog-ignore-db=mysql
## 开启二进制日志功能
log-bin=mall-mysql-bin
## 设置二进制日志使用内存大小（事务）
binlog_cache_size=1M
## 设置使用的二进制日志格式（mixed,statement,row）
binlog_format=mixed
## 二进制日志过期清理时间。默认值为0，表示不自动清理。
expire_logs_days=7
## 跳过主从复制中遇到的所有错误或指定类型的错误，避免slave端复制中断。
## 如：1062错误是指一些主键重复，1032错误是因为主从数据库数据不一致
slave_skip_errors=1062

```

- 重启mysql-master容器

```
sudo docker restart mysql-master
```

- 进入mysql-master容器

```
sudo docker exec -it mysql-master /bin/bash
```

- master容器实例内创建数据同步用户

```
mysql -uroot -p
CREATE USER 'slave'@'%' IDENTIFIED BY '123456';
GRANT REPLICATION SLAVE, REPLICATION CLIENT ON *.* TO 'slave'@'%';

ALTER USER 'slave'@'%' IDENTIFIED WITH mysql_native_password BY '123456';
```

- 查看主机状态

```
show master status;
```



##### 从服务器

- 新建从服务器3307

```
sudo docker run -p 3307:3306 --name mysql-slave -v /home/ubuntu/mysql/mysql-slave/log:/var/log/mysql -v /home/ubuntu/mysql/mysql-slave/data:/var/lib/mysql -v /home/ubuntu/mysql/mysql-slave/conf:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD=root -d mysql
```

- 进入/home/ubuntu/mysql/mysql-slave/conf 新建my.cnf

```
cd /home/ubuntu/mysql/mysql-slave/conf
sudo vim my.cnf

[mysqld]
## 设置server_id，同一局域网中需要唯一
server_id=102
## 指定不需要同步的数据库名称
binlog-ignore-db=mysql
## 开启二进制日志功能，以备Slave作为其它数据库实例的Master时使用
log-bin=mall-mysql-slave1-bin
## 设置二进制日志使用内存大小（事务）
binlog_cache_size=1M
## 设置使用的二进制日志格式（mixed,statement,row）
binlog_format=mixed
## 二进制日志过期清理时间。默认值为0，表示不自动清理。
expire_logs_days=7
## 跳过主从复制中遇到的所有错误或指定类型的错误，避免slave端复制中断。
## 如：1062错误是指一些主键重复，1032错误是因为主从数据库数据不一致
slave_skip_errors=1062
## relay_log配置中继日志
relay_log=mall-mysql-relay-bin
## log_slave_updates表示slave将复制事件写进自己的二进制日志
log_slave_updates=1
## slave设置为只读（具有super权限的用户除外）
read_only=1

```

- 重启msyql-slave容器

```
sudo docker restart mysql-slave
```

- 进入到msyql-slave中

```
sudo docker exec -it mysql-slave /bin/bash
mysql -uroot -p
```

- 配置主从复制

```
change master to master_host='宿主机ip',master_user='slave',master_password='123456',master_port=3306,master_log_file='mall-mysql-bin.000001', master_log_pos=617, master_connect_retry=30;

change master to master_host='43.142.112.65',master_user='slave',master_password='123456',master_port=3306,master_log_file='mall-mysql-bin.000001', master_log_pos=1688, master_connect_retry=30;
```

- 在从数据库中查看主从复制状态

```
show slave status\G;

其中
Slave_IO_Running: No
Slave_SQL_Running: No

```

- 在从数据库中开启主从复制

```
start slave
```

- 在从数据库中查看主从复制状态

```
show slave status\G;

其中
Slave_IO_Running: Yes
Slave_SQL_Running: Yes
```

面试题：1-2亿条数据需要缓存，请问如何设计这个存储案例“

回答： 单机无法实现，采用分布式存储。

- 哈希取余分区
  - 优点：简单粗暴，直接有效，只需要预估好数据规划好节点，例如3台、8台、10台，就能保证一段时间的数据支撑。使用Hash算法让固定的一部分请求落到同一台服务器上，这样每台服务器固定处理一部分请求(并维护这些请求的信息)，起到负载均衡+分而治之的作用。
  - 缺点：原来规划好的节点，进行扩容或者缩容就比较麻烦，不管扩缩，每次数据变动导致节点有变动，映射关系需要重新进行计算，在服务器个数固定不变时没有问题，如果需要弹性扩容或故障停机的情况下，原来的取模公式就会发生变化：Hash(key)/3会变成Hash(key) /?。此时地址经过取余运算的结果将发生很大变化，根据公式获取的服务器也会变得不可控。
    某个redis机器宕机了，由于台数数量变化，会导致hash取余全部数据重新洗牌。
- 一致性哈希算法分区
  - 背景：一致性哈希算法在1997年由麻省理工学院提出，设计目的是为了解决分布式缓存数据变动和映射问题，某个机器宕机了，分母数量改变，自然取余数就存在问题。
  - 3大步骤
    - 算法构建一致性哈希环
    - 服务器IP节点映射
    - key落到服务器的落键规则
  - 优点
    - 一致性哈希算法的容错性
    - 一致性哈希算法的扩展性
  - 缺点
    - 一致性哈希算法的数据倾斜问题：在服务器节点太少时，容易因为节点分布不均匀而造成数据倾斜（被缓存的对象大部分集中缓存在一台服务器上）问题。
- 哈希槽分区
  - 哈希槽实质上是一个数组[0,2^14-1]形成hash slot空间 16384个槽位（0-16383）
  - 可以解决均匀分配的问题，在数据和节点之间又加了一层，把这层称为哈希槽（slot），用于管理数据和节点之间的关系，现在相当于节点上放的是槽，槽里放的是数据。

### redis集群

##### 集群配置

```
配置三主三从
master1 6379-	slave1 6383
master2 6380-	slave2 6384
master3 6381-	slave3 6382
```

- 新建6台docker容器启动redis

```
sudo docker run -d --name redis-node-1 --net host --privileged=true -v /home/ubuntu/redis/share/redis-node-1/:/data redis --cluster-enabled yes --appendonly yes --port 6379

sudo docker run -d --name redis-node-2 --net host --privileged=true -v /home/ubuntu/redis/share/redis-node-2/:/data redis --cluster-enabled yes --appendonly yes --port 6380

sudo docker run -d --name redis-node-3 --net host --privileged=true -v /home/ubuntu/redis/share/redis-node-3/:/data redis --cluster-enabled yes --appendonly yes --port 6381

sudo docker run -d --name redis-node-4 --net host --privileged=true -v /home/ubuntu/redis/share/redis-node-4/:/data redis --cluster-enabled yes --appendonly yes --port 6382

sudo docker run -d --name redis-node-5 --net host --privileged=true -v /home/ubuntu/redis/share/redis-node-5/:/data redis --cluster-enabled yes --appendonly yes --port 6383

sudo docker run -d --name redis-node-6 --net host --privileged=true -v /home/ubuntu/redis/share/redis-node-6/:/data redis --cluster-enabled yes --appendonly yes --port 6384
```

- 为6台机器构建集群关系

```
sudo docker exec -it redis-node-1 /bin/bash

# 本地部署
redis-cli --cluster create 10.0.4.14:6379 10.0.4.14:6380 10.0.4.14:6381 10.0.4.14:6382 10.0.4.14:6383 10.0.4.14:6384 --cluster-replicas 1

# 远程部署
redis-cli --cluster create 43.142.112.65:6379 43.142.112.65:6380 43.142.112.65:6381 43.142.112.65:6382 43.142.112.65:6383 43.142.112.65:6384 --cluster-replicas 1
```

**集群总线**

```
每个Redis集群中的节点都需要打开两个TCP连接。一个连接用于正常的给Client提供服务，比如6379，还有一个额外的端口（通过在这个端口号上加10000）作为数据端口，例如：redis的端口为6379，那么另外一个需要开通的端口是：6379 + 10000， 即需要开启 16379。16379端口用于集群总线，这是一个用二进制协议的点对点通信信道。这个集群总线（Cluster bus）用于节点的失败侦测、配置更新、故障转移授权，等等。
```

- 查看集群状态

```
cluster info 
cluster nodes
```

##### 主从容错切换迁移

- 数据读写存储，以集群环境连接redis

```
redis-cli -p 6379 -c
```

查看集群信息

```
redis-cli --cluster check 10.0.4.14:6379 
```

- 容器切换迁移
  - 主节点宕机，从节点变主机
  - 主节点恢复，变为从机

##### 扩容

- 新建两个redis容器

```
sudo docker run -d --name redis-node-7 --net host --privileged=true -v /home/ubuntu/redis/share/redis-node-7/:/data redis --cluster-enabled yes --appendonly yes --port 6385

sudo docker run -d --name redis-node-8 --net host --privileged=true -v /home/ubuntu/redis/share/redis-node-8/:/data redis --cluster-enabled yes --appendonly yes --port 6386
```

- 进入到7号容器实例内部

```
sudo docker exec -it redis-node-7 /bin/bash
```

- 将新增的6385节点（空槽位）作为master节点加入集群

```
redis-cli --cluster add-node 10.0.4.14:6385 10.0.4.14:6379
通过redis-cli --cluster check 10.0.4.14:6385查看集群信息可以发现当前7号主机没有槽位，没有从机
10.0.4.14:6385 (c8e1715f...) -> 0 keys | 0 slots | 0 slaves.

```

- 重新分配槽位

```
redis-cli --cluster reshard 10.0.4.14:6380 

How many slots do you want to move (from 1 to 16384)? 4096
What is the receiving node ID? c8e1715f40773a59da732b3296540656c74bb1d0
Please enter all the source node IDs.
  Type 'all' to use all the nodes as source nodes for the hash slots.
  Type 'done' once you entered all the source nodes IDs.
Source node #1: all

```

![image-20221128235016555](C:\Users\xiaom\AppData\Roaming\Typora\typora-user-images\image-20221128235016555.png)

- 为主节点6385分配从节点6386

```
redis-cli --cluster add-node 10.0.4.14:6386 10.0.4.14:6385 --cluster-slave --cluster-master-id c8e1715f40773a59da732b3296540656c74bb1d0
```

- 检查集群状态

```
redis-cli --cluster check 10.0.4.14:6385
```

![image-20221129132900842](C:\Users\xiaom\AppData\Roaming\Typora\typora-user-images\image-20221129132900842.png)

##### 缩容

- 删除从节点6379

```
redis-cli --cluster del-node 10.0.4.14:6379 e030e314ea951b772e259fc16ee08223aa5e09e2
```

- 将主节点6383的槽号清空，重新分配，本例将请出来的槽号都给6380

```
redis-cli --cluster reshard 10.0.4.14:6380 
```

![image-20221129134648254](C:\Users\xiaom\AppData\Roaming\Typora\typora-user-images\image-20221129134648254.png)

- 将主节点6383删除

```
redis-cli --cluster del-node 10.0.4.14:6383 2722a126cd2ecac86f3bd986db0558f9e3db626c
```

### DockerFile

dockerfile是用来构建docker镜像的文本文件，是由一条条构建镜像所需的指令和参数构成的脚本。

构建三步曲

1. 编写dockerfile文件
2. docker build命令构建镜像
3. docker run依镜像运行容器实例

##### 基础知识

- 每条保留字指令都必须为大写字母且后面要跟随至少一个参数
- 指令依照从上到下，顺序执行
- `#` 表示注释
- 每条指令都会创建一个新的镜像层并对镜像进行提交

##### 保留字

- FROM -----基础镜像，当前新镜像是基于哪个镜像的，指定一个已经存在的镜像作为模板，第一条必须是from
- MAINTAINER -----镜像维护者的姓名和邮箱地址
- RUN
  - 容器构建时需要执行的命令
  - 两种格式
    - shell   `RUN <command>`
    - exec    `RUN ['executable','param1','param2']`
  - RUN时在docker build时运行
- EXPOSE-----当前容器对外暴露的端口
- WORKDIR------指定在创建容器后，终端默认登陆的进来工作目录，一个落脚点
- USER-----指定该镜像以什么样的用户去执行，如果都不指定，默认是root
- ENV-----用来在构建镜像过程中设置环境变量
- VOLUME-----容器数据卷，用于数据保存和持久化工作
- ADD------ 将宿主机目录下的文件拷贝进镜像且会自动处理URL和解压tar压缩包
- COPY
  - 类似ADD，拷贝文件和目录到镜像中。 将从构建上下文目录中 <源路径> 的文件/目录复制到新的一层的镜像内的 <目标路径> 位置
  - COPY src dest
  - COPY ["src", "dest"]
  - <src源路径>：源文件或者源目录
  - <dest目标路径>：容器内的指定路径，该路径不用事先建好，路径不存在的话，会自动创建。
- CMD
  - 容器启动命令
    - shell   `CMD <command>`
    - exec    `CMD ['executable','param1','param2']`
    - 参数列表形式： `CMD [param1','param2']`在制定了ENTRYPOINT指令后，用CMD指定具体的参数
  - Dockerfile 中可以有多个 CMD 指令，但**只有最后一个生效，CMD 会被 docker run 之后的参数替换**
- ENTRYPOINT
  - 也是用来指定一个容器启动时要运行的命令
  -  类似于 CMD 指令，但是ENTRYPOINT不会被docker run后面的命令覆盖， 而且这些命令行参数会被当作参数送给 ENTRYPOINT 指令指定的程序
  - 优点：在执行docker run的时候可以指定 ENTRYPOINT 运行所需的参数

##### 案例

创建自己的centos，要求具有vim，ifconfig，python功能

1. 编写Dockerfile文件，D大写

```
FROM centos
MAINTAINER wxm<xiaomeng23@126.com>

ENV MYPATH /usr/local
WORKDIR $MYPATH

#安装vim编辑器
RUN yum -y install vim
#安装ifconfig命令查看网络IP
RUN yum -y install net-tools
#安装python
RUN mkdir /usr/local/python
#ADD 是相对路径jar,把Python-3.10.8.tgz添加到容器中,安装包必须要和Dockerfile文件在同一位置
ADD Python-3.10.8.tgz /usr/local/python/
#配置python环境变量
ENV PYTHON_HOME /usr/local/python/Pyth-3.10.8
ENV PATH $PYTHON_HOME/bin:$PATH

EXPOSE 80
CMD echo $MYPATH
CMD echo "success--------------ok"
CMD /bin/bash

```

2. 构建镜像

```
sudo docker build -t 新镜像名字：TAG.

sudo docker build -t centospython:1.1. /home/ubuntu/myfile/
```

3. 运行新构建的镜像

```
sudo docker run -it 546c15103b9a
```





​		

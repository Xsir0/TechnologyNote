### Docker容器的基本操作

#### 1. 启动容器

- 启动单个 

  `docker run ubuntu echo 'hello world'`

- 启动交互式容器

  `docker run -i -t IMAGE/bin/bash`  进入容器

  注: -i --interactive=true|false 默认false

#### 2. 查看容器
- `docker ps [-a] [-l]`
  	注:`-a`列出所有的容器;`-l`列出最新创建的容器;不指定参数时返回的是正在运行中的容器

- `docker inspect [containerID | containerNAME] `查看某一指定容器详细信息

#### 3. 运行是指定容器的名字

- `docker run --name=container1 -i -t ubuntu /bin/bash`

#### 4. 重新启动已经停止的容器

- `docker start [-i] containerNAME`

#### 5. 删除停止的容器

-  `docker rm containerNAME`(只能删除已经停止的容器)

  
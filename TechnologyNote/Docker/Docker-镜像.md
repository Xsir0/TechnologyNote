### Docker-镜像

#### 列出镜像

- `docker images [OPTIONS] [REPOSITORY]`

  `-a --all=false`

  `-f --filter=[]`

  `--no-trunc=false`

  `-q --quiet=false`

  

#### 仓库 [Repository]



#### 查看镜像的详细信息

- `docker inspect [OPTIONS] CONTAINER|IMAGE[CONTAINER|IMAGE...]`

  `-f --format=""`

#### 删除镜像

- `docker rmi [OPTIONS] IMAGE [IMAGE...]`

  `-f --force=false Force removal of the image`

  `--no-prune=false Do not delete untagged parents`

#### 查找镜像

1.  [Docker Hub](https://registry.hub.docker.com)

2. docker search [OPTION] TERM

   - --automated=false   -- Only show automated builds
   -  --no-trunc=false  --- Don't truncate output
   -  --s --stars=0   --- Only displays with at least x stars

   `注:最多返回25个结果`

#### 拉取镜像

- `docker pull [OPTIONS] NAME[:TAG]`

  `-a --all-tags=false Download all tagged images in the repository`

- 使用 `--registry-mirror` 选项

  1. 修改:`/etc/default/docker`
  2. 添加:`DOCKER_OPTS="--registry-mirror=http://MORROR-ADDR"`

#### 构建镜像

1. 通过容器构建镜像

   - `docker commit [OPTIONS] COMTAINER [REPOSITORY[:TAG]]`

     `-a --author="" Author`

     `-m --message="" Commit message`

     `-p --pause=true Pause container during commit`

2. 通过Dockerfile文件构建

   - `docker build`
     1. 创建dockerfile文件

   > #First dockerfile for test
   >
   > FROM ubuntu:14.04
   > MAINTAINER xiesir
   > RUN apt-get update
   > RUN apt-get install -y nginx
   > EXPOSE 80

   ​		2. `docker build [OPTIONS] PATH |URL| -`

   ​	`--FORCE-RM=false`

   ​	`--no-cache=false`

   ​	`--pull=false`

   ​	`-q --quiet=false`

   ​	`--rm=true`

   ​	`-t --tag=""`

最终运行 : `docker run -d --name nginx_web2 -p 80 xiesir/df_test1 nginx -g "daemon off;"`
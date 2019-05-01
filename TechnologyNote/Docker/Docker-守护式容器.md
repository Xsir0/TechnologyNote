### Docker - 守护式容器

#### 以守护形式运行容器

- `docker run -i -t IMAGE /bin/bash`

  使用`Ctrl+P`和`Ctrl+Q`的组合键退出交互容器的bash

#### 再次进入已经退出了的容器

- `docker attach containerNAME`

#### 启动守护式容器

- `docker run -d IMAGE [COMMAND] [ARG...]`

  注: `-d` 告诉后台启动容器时使用后台运行的方式

#### 查看容器日志

- `dockere logs [-f] [-t] [--tail] containerNAME`

  注: `-f --follows=true|false`默认false  (一直跟踪日志的变化)

  ​	`-t --timestamps=true|false`  默认为false (再返回的结果上加上时间戳)

  ​	`--tail="all"`  (返回结尾处多少数量的日志)

#### 查看容器内进程

- `docker top containerNAME`

#### 在运行的容器中启动新进程

- `docker exec [-d] [-i] [-t] containerNAME [COMMAND] [ARG...]`

#### 停止守护式容器

- `docker stop containerNAME`  (发送命令给容器,等待容器的停止)
- `docker kill containerNAME` (直接停止容器)

#### 使用docker帮助文件

> man docker-run
>
> man docker-logs
>
> man docker-top
>
> man docker-exec
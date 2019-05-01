### Docker镜像与仓库

#### Dockerfile指令

\#  Comment(注释)

 **INSTRUCTION** argument  [指令名   参数]

- FROM
  - FROM<image>
  - FROM<image>:<tag>

- MAINTARINER

  - 指定镜像的作者信息,包含镜像的所有者和联系信息

- RUN
  - 指定当前镜像中运行的命令
  - RUN <command> (shell 模式)  eg:/bin/sh -c command    ::: RUN echo hello
  - RUN ["executable","param1","param2"]  (exec模式) eg:RUN["/bin/bash","-c","echo hello"]

- EXPOSE
  - 指定运行该镜像的容器使用的端口
  - EXPOSE<port> [<port>...]
  - 在容器运行时,仍然需要手动制定容器的端口号`docker run -p 80 -d xiesir/df_test1 nginx -g "daemon off;"`

  

以下命令用来指定容器运行时需要指定的命令

- CMD
  - CMD["executable","param1","param2"] (exec模式)
  - CMD command param1 param2 (shell模式)
  - 跟 `RUN`指令类似,但是`CMD`是在容器运行时执行,而`RUN`是在镜像构建的过程中执行
- ENTERPOINT
  - ENTERPOINT["executable","param1","param2"] (exec模式)
  - ENTERPOINT command param1 param2 (shell模式)



以下命令用来设置镜像的目录文件

- ADD

  - 将文件或目录添加到Dockerfile构建的镜像中
  - ADD <src> ...<dest>
  - ADD ["<src>"..."<dest>"] (适用于文件路径中有空格的情况)

- COPY

  - 将文件或目录添加到Dockerfile构建的镜像中
  - ADD <src> ...<dest>
  - ADD ["<src>"..."<dest>"] (适用于文件路径中有空格的情况)

  ADD vs.COPY 两者区别: 

  - ADD 包含类似tar的解压功能
  - 如果单纯复制文件,Docker推荐使用COPY

- VOLUME

  - 向基于镜像创建的容器添加卷



以下命令用来制定镜像构建以及容器运行时的环境设置

- WORKDIR
  - 通过镜像创建一个新容器时,在容器内部创建工作目录
  - `WORKDIR /path/to/workdir`  通常使用绝对路径

- ENV

  - 用来制定环境变量,与`WORKDIR`指令类似
  - ENV<key><value>
  - ENV<key>=<value>...
  - 在构建和运行过程中都有效

- USER

  - 用来指定镜像会以什么样的用户来运行
  - USER daemon

  还可以通过一下方式运行

  - USER user
  - USER uid
  - USER user:group
  - USER uid:gid
  - USER user:gid
  - USER uid:group

  不指定用户时,默认会使用root用户

类似触发器指令

- ONBUILD
  - 为镜像添加触发器
  - 当一个镜像被当做其它镜像的基础镜像时会执行
  - 并不会在本次镜像被构建是执行

#### Dockerfile构建过程

- 从基础镜像运行一个容器
- 执行一条指令,对容器作出修改
- 执行类似`docker commit`的操作,提交一个新的镜像层
- 再基于刚提交的镜像运行一个新容器
- 执行Dockerfile中的下一条指令,直至所有指令执行完毕

不使用构建过程中的缓存时,使用`docker build  --no-cache ` 命令



##### 对给定的镜像,查看构建过程

`docker history [image]`
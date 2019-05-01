### Docker容器的数据管理

#### Docker容器的数据卷

> docker的生命周期跟容器中运行的程序相一致的

> 数据卷是经过特殊设计的目录,可以绕过联合文件系统,为一个或多个容器提供访问.

> 数据卷设计的目的,在于数据的永久化,它完全独立于容器的生命周期,因此,docker不会再容器删除时删除其挂载的数据卷,也不会存在类似的垃圾回收机制,对容器引用的数据卷进行处理.

#### 数据卷的特点

- 数据卷在容器启动时初始化,如果容器使用的镜像在挂载点包含了数据,这些数据会拷贝到新初始化的数据卷中.
- 数据卷可以在容器之间共享和重用
- 可以对数据卷里的内容直接进行修改
- 数据卷的变化不会影响镜像的更新
- 卷会一直存在,即使挂载数据卷的容器已经被删除

#### 为容器添加数据卷

`sudo docker run -v ~/container_data:/data -it ubuntu /bin /bash`

#### 为数据卷添加访问权限

`sudo docker run -v ~/datavolume:/data:ro -it ubuntu /bin/bash`

#### 使用Dockerfile构建包含数据卷的镜像

`VOLUME ["/data"]`

#### Docker的数据卷容器

> 命名的容器挂载数据卷,其他容器通过挂载这个容器实现数据共享,挂载数据卷的容器,就叫数据卷容器

#### 挂载数据卷容器的方法

`docker run --volumes-from [CONTAINER NAME]`

#### Docker数据卷的备份和还原(需重新学习)

- 数据备份方法
  - `docker run --volumes-from [container name] -v $(pwd):/backup ubuntu tar cvf /backup/backup.tar [container data volume]`

![1554638274110](/home/xsir/.config/Typora/typora-user-images/1554638274110.png)

- 数据还原方法
  - `docker run --volumes-from [container name] -v $(pwd):/backup ubuntu tar xvf /backup/backup.tar [container data volume]`
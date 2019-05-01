### ubuntu 安装docker

1. 安装命令 `sudo apt-get install docker`
2. 检查 `docker` 版本  `sudo docker version`
3. 运行 `docker`  `sudo run ubuntu  echo  'hello world'`
4. 用非root用户用户权限运行docker
   1. 创建docker用户组    `sudo groupadd docker`
   2. 将当前登录用户添加到docker用户组  `sudo gpasswd -a $USER docker`
   3. 更新用户组 newgrp docker
   4. 测试运行   `docker run ubuntu echo 'Hello world'`

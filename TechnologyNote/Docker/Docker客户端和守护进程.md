### Docker客户端和守护进程

#### Docker的CS模式

![Docker的C/S模式 - Client](/home/xsir/.config/Typora/typora-user-images/1554599258042.png)

#### Remote API

- RESTful 风格API

[ Docker官方的Remote API Reference](https://docs.docker.com/reference/api/docker_remote_api/)



#### 连接方式(socket)

- unix:///var/run/docker.sock(默认)
- tcp://host:port
- fd://socketfd



#### Docker 守护进程的配置和操作

###### 查看守护进程

- `ps -ef | grep docker`
- `sudo status docker`

- `docker stats` [查看docker守护进程运行状态]

###### Docker的启动选项

> 启动项

- `-D  --debug=false`
- `-e  --exec-driver="native"`
- `-g  --graph="/var/lib/docker"`
- `--icc=true`
- `-l  --log-level="info"`
- `--label=[]`
- `-p  --pidfile="/var/run/docker.pid"`

> 服务器连接相关

- `-G  --group="docker"`
- `-H  --host=[]`

- `--tls=false`

- `--tlscacert="/home/sven/.docker/ca.pem"`

- `--tlscert="/home/sven/.docker/cert.pem"`

- `--tlskey="/home/sven/.docker/key.pm"`

- `--tlsverify=false`

> RemoteAPI相关

- `--api-enable-cors=false`

> 存储相关

- `-s   --storage-driver=""`

- `--selinux-enabled=false`

- `--storage-opt=[]`

> Registry相关

- `--insecure-registry=[]`

- `--registry-mirror=[]`

> 网络设置相关

- `-b  --bridge=""`

- `--bip=""`

- `--fixed-cidr=""`

- `--fixed-cidr-v6=""`

- `--dns=[]`

- `--dns-search=[]`

- `--ip=0.0.0.0`

- `--ip-forward=true`

- `--iptables=true`

- `--ipv6=false`

- `--mtu=0`

##### Docker启动配置文件

`/etc/default/docker`

#### Docker的远程访问

- 修改Docker守护进程启动选项

  - -H  `tcp://host:port`

    ​      `unix:///path/to/socket`

    ​    `fd://*` or `fd://socketfd`

- 守护进程默认配置:
  - -H `unux:///var/run/docker.sock`





















































































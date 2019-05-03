## ftp命令使用
### 远程文件传输的概念
### ftp的验证登录
### ftp的传输模式设置
### ftp的文件上传
### ftp的文件下载
- `mput test.txt` 从ftp服务器下载文件test.txt
- `mget test.txt` 上传文件至ftp服务器
- `!<commond>` 执行客户端命令
- `<commond>` 执行ftp服务端命令
## ftp服务的安装
- ftp服务在线安装
    - `apt-get install vsftod`
- ftp服务离线安装
    - `dpkg -i vsftpd*.deb`

## ftp服务的启停和配置
- ftp服务的启动 
    - `service vsftpd start`
- ftp服务的停止
    - `service vsftpd stop`
- ftp服务的重启
    - `service vsftpd restart`
- ftp服务的配置文件
    - `/etc/vsftpd.conf`
## ssh的命令使用
### 远程安全登录的概念
### 使用ssh远程安全登录
- ssh是客户端命令
- ssh仅提供远程安全登录的本地会话窗口
### ssh服务的安装
- ssh服务在线安装: 
    - `apt-get install openssh-server`
- ssh服务离线安装
    - `dpkg -i openssh-server*.deb`
### ssh服务的启停和配置
- ssh服务的启动:
    - `service ssh start`
- ssh服务的停止:
    - `service ssh stop`
- ssh服务的重启:
    - `service ssh restart`
- ssh服务的配置文件
    - `/etc/ssh/sshd_conf`
## Linux用户管理
### 用户添加与删除
- 用户添加命令 : `useradd`
    - 常用选项参数 `-m` 用于添加用户的同事创建爱你该用户的家目录
    -  eg: `useradd -m testuser`
- 用户删除命令 : `userdel`
    - 常用选项参数 `-r` 用于删除用户的同时删除包括该用户家目录的所有文档
        - eg : `userdel -r testuser`
- 为创建的用户添加密码: `sudo passwd testuser`
### 用户查看
- 查看当前用户命令 : `whoami`
- 查看所有登录用户命令 : `who`
- 用户id查看命令: `id`
    - 缺省显示当前用户所有的id信息
    - 常用选项参数 `-u` 用于仅显示当前的有效用户id
        - eg : `id -u`
        - eg : `id -u testuser`
### 用户切换
- 用户间切换命令: `su <username>`
-  在ubuntu系统中,su用户后通常需要输入该用户的口令,但有例外:
    - 超级用户su任何用户,无需输入该用户的口令
- 在ubuntu系统中,切换到root用户的推荐方法: `sudo -i`
- 用户临时获取管理员授权的命令: `sudo <commondName>`
    - 在ubuntu系统中,sudo命令提交后通常需要输入管理口令,但也有例外
        - 在统一窗口缓存时间内,无需多次输入口令
- 在ubuntu系统中,sudo命令的使用有用户限制
    - 将用户添加至sudo用户组:
        - `gpasswd -a testuser sudo`
### 用户账户锁定
- 用户账户的锁定: `usermod -L`
- 用户账户的解锁: `usermod -U`
### 用户账户配置文件
- 用户账号文件 : `/etc/passwd`
- 用户影子密码文件 : `/etc/shadow`

### 用户组增删与查看
#### 用户组添加与删除
- 用户组添加: `groupadd`
    - 缺省分配当前未被占用的最小gid给新用户组
    - 常用选项参数`-g` 用于指定新用户组的gid
        - eg:  `groupadd -g <gid>`
- 用户组删除: `groupdel`
    - 删除指定的未被占用的用户组
        - eg: `groupdel testgroup`
    - 组的账号文件 `/etc/group`
#### 用户组查看
- 用户组查看命令: `groups`
    - 缺省查看当前用户所在的所有用户组
    - 指定用户名时,查看指定用户所在的用户组
    - eg: `groups <username>`
#### 用户组成员更改
- 用户组成员更改:   `gpasswd <groupName>`
    - 常用选项参数 `-a` 用于将新增用户加入组群
        - eg:  `gpasswd -a <username> <groupName>`
    - 常用选项参数 `-d` 用于将用户从该组群删除
        - eg: `gpasswd -d <username> <groupName>`
- 改变有效登录群组: `newgrp <groupName>`

#### 用户组的配置问文件
- 用户组账号文件 `/etc/group`
- 用户组影子文件 `/etc/gshadow`
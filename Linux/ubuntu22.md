### 1. 新用户设置root密码
    sudo passwd

### 2. 修改为清华源镜像
```shell
## 2. 修改为清华镜像源  
[清华镜像站官网](https://mirror.tuna.tsinghua.edu.cn/help/ubuntu/) 
    ```shell
    # 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
    deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy main restricted universe multiverse
    # deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy main restricted universe multiverse
    deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse
    # deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-updates main restricted universe multiverse
    deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse
    # deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-backports main restricted universe multiverse

    # 以下安全更新软件源包含了官方源与镜像站配置，如有需要可自行修改注释切换
    deb http://security.ubuntu.com/ubuntu/ jammy-security main restricted universe multiverse
    # deb-src http://security.ubuntu.com/ubuntu/ jammy-security main restricted universe multiverse

    # 预发布软件源，不建议启用
    # deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-proposed main restricted universe multiverse
    # # deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ jammy-proposed main restricted universe multiverse
    ```
a. 备份镜像源 cp /etc/apt/sources.list /etc/apt/sources.list.bak  
b. vim /etc/apt/sources.list  
c. 更新镜像源   
d. sudo apt-get update 
    * 若更新失败，则在/etc/netplan/01-network-manager-all.yaml添加域名8.8.4.4 
    ```
### 3. ssh登陆  
    apt install firewalld openssh-client openssh-server
    firewall-cmd --permanent --add-port=22/tcp
    firewall-cmd --reload
    cd /etc/ssh/sshd_config
    将PermitRootLogin prohibit-password 改为 PermitRootLogin yes
    重启ssh服务：sudo systemctl restart ssh
    vim /etc/ssh/sshd_config

    ssh免密登录:
    ssh-keygen
    vim authorized_keys

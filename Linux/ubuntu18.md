## 1. ubuntu虚拟机网络设置
### 1.1 NAT模式（静态方式）
    a. 在vmware虚拟网络编辑器中添加nat设置（以管理员打开）
        * 添加网络VMnet8, NAT模式
        * 勾选上“将主机适配器连接到此网络”
        * 不勾选“使用本地DHCP服务将ip地址分配给虚拟机”
        * 设置子网ip, 如192.168.100.0, 网关为192.168.100.2， 主机IP为192.168.100.1（VmNet8的ip地址）

    b. 打开主机网络适配器，将热点网络共享给VMnet8

    c. 将VMnet8的ip设置为192.168.100.1

    d. 打开ubuntu虚拟机
        * cd /etc/netplan
        * vim 01-network-manager-all.yaml
        * dhcp4改为no, addresses改为ubuntu的ip（192.168.100.100）
        * 网关改为192.168.100.2
        * 保存配置信息：sudo netplan apply
        * 测试主机和虚拟机之间的连通性 ping 192.168.100.100
        * ping www.baidu.com测试 
  ```py
  network:
  version: 2
  renderer: NetworkManager
  ethernets:
          ens33:
                  dhcp4: no
                  dhcp6: no
                  addresses: [192.168.100.100/24]
                  gateway4: 192.168.100.2
                  nameservers:
                          addresses: [114.144.114.114, 8.8.8.8, 8.8.4.4]

```
### 1.2 桥接模式
    a. 本地主机ipconfig，查看热点名称，ip地址，网关地址
    b. 虚拟机设置中，选择桥接模式后，要勾选复制物理网络连接状态
    c. 在vmware虚拟网络编辑器中添加桥接模式, 桥接至热点的网卡
    d. 在/etc/netplan/01-network-manager-all.yaml中修改ip为热点ip所在网络，网关修改为热点的网关
    e, sudo  netplan apply
    e. ping wwww.baidu.com，测试连通性

## 2. 修改为清华镜像源  
[清华镜像站官网](https://mirror.tuna.tsinghua.edu.cn/help/ubuntu/) 
```shell
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse

# 以下安全更新软件源包含了官方源与镜像站配置，如有需要可自行修改注释切换
deb http://security.ubuntu.com/ubuntu/ bionic-security main restricted universe multiverse
# deb-src http://security.ubuntu.com/ubuntu/ bionic-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
# # deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
```
    a. 备份镜像源 cp /etc/apt/sources.list /etc/apt/sources.list.bak  
    b. vim /etc/apt/sources.list  
    c. 更新镜像源   
    d. sudo apt-get update 
        * 若更新失败，则在/etc/netplan/01-network-manager-all.yaml添加域名8.8.4.4 

## 3. ubuntu设置ssh远程登录
[远程登录教程](https://blog.csdn.net/qq_20147559/article/details/140650080)

## 4. mysql安装[](https://blog.csdn.net/haixiangyun/article/details/132597777)
   1） sudo apt install mysql-server
   2） 查看MySQL服务状态：sudo service mysql status
　  　查看MySQL版本号：sudo mysql
   3） set password for 'root'@'localhost' = password('root');
   4) 设置MySQL允许远程登录：GRANT ALL PRIVILEGES ON *.* TO 'root'@'%'IDENTIFIED BY 'Admin@123' WITH GRANT OPTION;
   5) 先停掉mysql服务，否则无法修改配置文件：sudo service mysql stop
   6) 修改配置文件：sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
   7) 启动mysql服务：　sudo service mysql start
   8) 设置mysql自动启动： sudo systemctl start mysql



















## 3. vim快捷键 
**定位到某行：输入行号+G**
### 模式切换
- **`i`**：进入插入模式。PPPP
- **`Esc`**：返回普通模式。
- **`v`**：进入可视模式。
- **`V`**：进入行可视模式。
- **`Ctrl+v`**：进入块可视模式。

### 基本移动
- **`h`**：左移一个字符。
- **`j`**：下移一行。
- **`k`**：上移一行。
- **`l`**：右移一个字符。
- **`w`**：移动到下一个单词的开头。
- **`b`**：移动到上一个单词的开头。
- **`e`**：移动到当前单词的末尾。
- **`0`**：移动到行首。
- **`$`**：移动到行尾。
- **`gg`**：移动到文件开头。
- **`G`**：移动到文件末尾。

### 编辑
- **`x`**：删除当前字符。
- **`dw`**：删除一个单词。
- **`dd`**：删除当前行。
- **`yy`**：复制当前行。
- **`p`**：粘贴。
- **`u`**：撤销。
- **`Ctrl+r`**：重做。

### 搜索和替换
- **`/pattern`**：向前搜索`pattern`。
- **`?pattern`**：向后搜索`pattern`。
- **`n`**：跳转到下一个搜索结果。
- **`N`**：跳转到上一个搜索结果。
- **`:s/old/new`**：将当前行中的第一个`old`替换为`new`。
- **`:s/old/new/g`**：将当前行中的所有`old`替换为`new`。
- **`:%s/old/new/g`**：将整个文件中的所有`old`替换为`new`。

### 文件操作
- **`:w`**：保存文件。
- **`:q`**：退出。
- **`:wq`**：保存并退出。
- **`:q!`**：不保存强制退出。
- **`:e filename`**：打开`filename`文件。
- **`:r filename`**：在当前文件中插入`filename`文件的内容。

### 高级操作
- **`Ctrl+o`**：返回到之前的位置。
- **`Ctrl+i`**：前进到下一个位置。
- **`:%y+`**：将整个文件复制到系统剪贴板。
- **`Ctrl+v`**然后选择区域，按`I`进入插入模式，再输入内容，按`Esc`将内容插入到选中区域每一行的开头。
- **`:split`**或**`:vsplit`**：水平或垂直分割窗口。

### 标签操作
- **`:tabnew`**：打开新标签页。
- **`:tabnext`**或**`:tabn`**：切换到下一个标签页。
- **`:tabprevious`**或**`:tabp`**：切换到上一个标签页。
- **`:tabclose`**：关闭当前标签页。

## 4. vmware tools：虚拟机与主机之间复制黏贴
    1） 点击左上角虚拟机的重新安装vmware tools
    2) 界面会弹出vmware tools的压缩包，将其复制到其他目录
    3) 解压，并进入vmware-tools-distrib
    4）执行sudo ./vwmware-install.pl
    4) 重启系统
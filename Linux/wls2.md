## 一、安装wsl
### 1. windows环境设置
[执行前五步](https://learn.microsoft.com/zh-cn/windows/wsl/install-manual)
同时更新nvidia显卡驱动

### 2. 安装和迁移wsl教程
[教程](https://blog.csdn.net/imok1234567/article/details/136820228)
将pip设置为清华源：pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

nvcc -V: 查看cuda的版本 
nvidia-smi

## 二、wsl的使用
**在文件夹管理器中键入 \\wsl$ ，可在文件夹下查看ubuntu的文件**

1. git远程克隆github项目  
    要在~/.ssh目录下添加config文件
    vim config
    ```vim
    Host github.com
    User yang1294891635@gmail.com
    Hostname ssh.github.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_ed25519
    Port 443
    ```

### 关闭wsl2：wsl --shutdown
### 重启wsl: wsl


### 4. wsl通过挂载访问win的数据集
ln -s /mnt/c/datasets/my_dataset ~/datasets/my_dataset

ln -s /mnt/d/image_registration/MegaDepth_v1/phoenix ~/datasets/megadepth/phoenix
ln -s /mnt/d/image_registration/MegaDepth_v1/phoenix ~/datasets/megadepth
D:\image_registration\MegaDepth_v1\phoenix


ln -sv /home/hry/datasets/megadepth/phoenix /home/ImageRegistration/LoFTR/data/megadepth/train

ln -s /mnt/d/image_registration/MegaDepth_v1/megadepth_indices ~/datasets/megadepth 

ln -sv /home/hry/datasets/megadepth/megadepth_indices /home/ImageRegistration/LoFTR/data/megadepth/index
D:\image_registration\MegaDepth_v1\megadepth_indices

G:\MegaDepth_v1
ln -sv /mnt/g/MegaDepth_v1 /datasets

ln -sv /datasets/MegaDepth_v1  ./dataset/megadepth

ln -sv /mnt/g/DenseUAV/DenseUAV /home/mapRegistration/DenseUAV-main/data
ln -sv /mnt/e/dataset/DenseUAV /home/mapRegistration/DenseUAV-main/data

ln -sv /mnt/e/dataset/self/dataset /home/mapRegistration/DenseUAV-main/data2


ln -sv /mnt/e/MegaDepth_v1_SfM ./dataset/megadepth/data2/
#### 硬盘挂载
sudo mkdir /mnt/g
sudo mount -t drvfs G: /mnt/g
sudo umount /mnt/g


#### cuda多版本安装
https://blog.csdn.net/m0_47532096/article/details/12927
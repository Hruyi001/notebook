### 1. anaconda安装
[安装教程](https://blog.csdn.net/fan18317517352/article/details/123035625)

### 2. anaconda的使用  
    1） 添加清华源
```
#添加镜像源
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/pro
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2

#终端显示包从哪个channel下载，以及下载地址是什么
conda config --set show_channel_urls yes
```

    2) 查看镜像源
    conda config --show channels

    3） 删除添加源、恢复默认源
    conda config --remove-key channels

### 3. pip的使用
    1） pip配置清华源
        * 配置临时清华源：
            # some-package代表你需要安装的包 
            pip install some-package -i https://pypi.tuna.tsinghua.edu.cn/simple 
        * 配置永久清华源：
            pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
    2） 国内常用的镜像源 
        pip install -i https://mirrors.aliyun.com/pypi/simple/ some-package 
            清华大学开源软件镜像站：https://pypi.tuna.tsinghua.edu.cn/simple
            阿里云开源镜像站：https://mirrors.aliyun.com/pypi/simple/
            豆瓣：https://pypi.douban.com/simple/
            中国科技大学 https://pypi.mirrors.ustc.edu.cn/simple/  

    3) 离线下载torch和torchvision
[离线下载](https://download.pytorch.org/whl/torch_stable.html)

    4) 删除指定环境：conda env remove --name env_name
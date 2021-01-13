# 基础环境搭建

## 一、Linux版本选择

*目前centos已经停止支持，所以建议选择ubuntu作为分析环境；选择还有开发者维护的环境可以避免很多未知错误导致软件安装失败或软件运行关联包的时候报错，故本系列笔记都是默认使用Ubuntu LTS*

## 二、Ubuntu初始环境配置

**安装完成后建议首先安装conda**

### 1、conda的安装

```shell
# 可以从清华源、中科大源、阿里源等等上下载下来
## 可以将下载任务挂载在后台
wget -b ...

# 下载后的安装包一般为 .gz 格式
## 首先解压
tar -zxvf ...

## 解压后会有一个 .sh 后缀的文件
## 直接bash ***.sh安装
bash ***.sh

## 注意：安装时避免选择直接安装到环境中，以免污染整个环境

## 将conda加入环境变量
echo export PATH=../../../bin:$PATH >> ~/.bashrc
source ~/.bashrc
```

### 2、conda镜像源的配置

```shell
# 首先是一个直接切换回默认镜像源的命令
conda config --remove-key channels

# channels的配置文件详情
vim ～/.condarc

# 已经配置好的清华镜像源
channels:
  - defaults
show_channel_urls: true
default_channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
custom_channels:
  conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud

# 添加镜像源时的命令
conda config --add channels "镜像源的地址" 

# 其他镜像源
```

其他镜像源

```shell
# 中科大镜像源
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/main/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/conda-forge/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/msys2/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/bioconda/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/menpo/
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/cloud/

# 阿里镜像源
conda config --add channels https://mirrors.aliyun.com/pypi/simple/

# 豆瓣的python的源
conda config --add channels http://pypi.douban.com/simple/ 

# 显示检索路径，每次安装包时会将包源路径显示出来
conda config --set show_channel_urls yes

conda config --set always_yes True

# 显示所有镜像通道路径命令
conda config --show channels
```



从国内镜像源下载包

```shell
# 更换后面的源路径和需要安装的包名即可
pip install -U pandas -i https://pypi.tuna.tsinghua.edu.cn/simple

pip install -U networkx python-louvain tensorflow-gpu==1.12 -i https://pypi.tuna.tsinghua.edu.cn/simple
```



### 3、Python的安装

*Ubuntu一般默认的python版本是2.x，但目前官方已经停止维护，所以更推荐使用3.x版本*

==除非特殊情况，尽量选择3.x版本的python==

```shell
apt-get install -y python
# 尽量安装最新版
```


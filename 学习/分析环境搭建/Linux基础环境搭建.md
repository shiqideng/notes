# 基础环境搭建

## 一、Linux版本选择

*目前centos已经停止支持，所以建议选择ubuntu作为分析环境；选择还有开发者维护的环境可以避免很多未知错误导致软件安装失败或软件运行关联包的时候报错*

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

```



### 3、Python的安装

```shell
apt-get install -y python
# 尽量安装最新版
```


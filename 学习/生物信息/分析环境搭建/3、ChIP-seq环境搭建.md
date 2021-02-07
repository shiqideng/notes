# ChIP-seq环境搭建

## 1、conda环境创建

```shell
conda create -n Chip-seq python=2

# 激活环境
conda activate Chip-seq
```

2、安装生信软件

```shell
conda install -y sra-tools  
conda install -y trim-galore  samtools
conda install -y deeptools homer  meme
conda install -y macs2 bowtie bowtie2 
```



https://www.gencodegenes.org/
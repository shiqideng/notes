# RNA-seq环境搭建
## conda创建环境

使用 conda创建一个rna环境，Python建议设置为2.x版本

```shell
conda create -n rna python=2

# 查看已有conda环境
conda info --envs

#conda激活某一个环境
source activate xxx
```

## 安装生信分析相关软件

```shell
# 激活已创建的rna环境
source activate rna

# 安装相关软件
conda install -y sratools bowtie2 bowtie
conda install -y samtools bwa subread
conda install -y cutadapt
```


# RNA-seq环境搭建

## 1、conda创建环境

使用 conda创建一个rna环境，Python建议设置为2.x版本

```shell
conda create -n rna python=2

# 查看已有conda环境
conda info --envs

#conda激活某一个环境
source activate xxx
```

## 2、安装生信分析相关软件

```shell
# 激活已创建的rna环境
source activate rna

# 安装相关软件
conda install -y sratools bowtie2 bowtie
conda install -y samtools bwa subread
conda install -y cutadapt
```

## 3、reference文件构建

#### （1）下载索引文件

```shell
# 通常使用的reference为hg19、hg38和mm10
# 索引文件可以直接从NCBI和Ensembl下载

# 下载地址（地址可能后面随着网站完善有所更改）
# hg19

# hg38

# mm10
```

#### （2）自己构建索引文件

bwa、bowtie、bowtie2使用的索引各不相同，所以需要分别构建索引

==注意：x和x在构建时还需要gtf或gff文件，所以需要单独下载==

#####  <1>下载hg19、hg38、mm10的fastq文件和gtf、gff文件

```shell

```

##### <2>构建索引

```shell

```


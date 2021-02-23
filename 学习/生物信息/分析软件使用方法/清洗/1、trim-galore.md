# Trim Galore使用方法

网址：http://www.bioinformatics.babraham.ac.uk/projects/trim_galore/

GitHub：https://github.com/FelixKrueger/TrimGalore

## 1、简介

Trim Galore是对cutadapt和FastQC的包装。适用于所有的高通量测序，包括RRBS（Reduced representation Bisulfite-Seq）、Illumina、Nextera和small RNA测序平台对双端和单端数据。主要功能包括两步：一、去除低质量碱基，然后去除`3'`末端的adapter，如果没有指定具体的adapter，程序会自动检测前`1 million`的序列，然后比对前12-13bp的序列是否符合一下类型的adapter：

Illumina：AGATCGGAAGAGC

Small RNA：TGGAATTCTCGG

Nextera：CTGTCTCTTATA

## 2、安装

可以直接源码安装或使用conda安装，不过需要注意的是==在安装前需要先安装cutadapt和fastqc==

```shell
源码安装：
# Check that cutadapt is installed
cutadapt --version
# Check that FastQC is installed
fastqc -v
# Install Trim Galore
## The Lastest relese is Version 0.6.6
curl -fsSL https://github.com/FelixKrueger/TrimGalore/archive/0.6.6.tar.gz -o trim_galore.tar.gz
tar xvzf trim_galore.tar.gz
# Run Trim Galore
~/TrimGalore-0.6.6/trim_galore
```

```shell
conda安装：
# Activate enviroment 'xxx'
conda activate xxx
# Install Trim Galore
conda install -y trim_galore
# Run Trim Galore
```

## 3、使用

示例：

```shell
## 处理双端测序结果
trim_galore -q 20 --phred33 --stringency 3 --length -e 0.1 --paired fastq1 fastq2\
--gzip -o outdir -a1 ATCG... -a2 ATCG...
```

参数说明：

-q/--quality：设定Phred quality score阈值，默认为20；

--phred33：选择--phred33或--phred64是根据测序数据版本决定的，`illumina 1.5`版本的quality score计算方式为ASCII+64，所以选择phred64，`illumina 1.9+`的版本quality score计算方式为ASCII+33，所以选择phred33；

-a/--adapter：输入adapter序列，默认为软件自带或自动读取前`1 million`个reads，比对计算得到adapter；a1后面为`3'`端引物，a2为`5'`端引物的反向互补序列；

--stringency：设定可以忍受的前后adapter重叠的碱基，默认为1（非常苛刻）。可以适度放宽，因为最后一个adapter几乎不可能被测序仪读到；

--length：设定输出reads长度阈值，小于设定值会被抛弃；

`--paired`：对于双端测序结果，一对reads中，如果有一个被剔除，那么另一个会被同样抛弃，而不管是否达到标准；

`--gzip`和`--dont_gzip`：清洗后的数据zip打包或者不打包；

`--output_dir`：输入目录。需要提前建立目录，否则运行会报错；

`-- trim-n` : 移除read一端的reads。
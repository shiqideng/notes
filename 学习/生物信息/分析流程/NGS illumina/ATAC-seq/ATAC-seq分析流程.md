# ATAC-seq分析流程

## 数据参考文章：

```
The landscape of accessible chromatin in mammalian preimplantation embryos. Nature 2016 Jun 30;534(7609):652-7. PMID: 27309802
```

## 数据GEO号：GSE66581

链接：https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE66581

因为全部文件很大，所以只选择四组数据作为练习

## 配置环境

```shell
# 建议使用conda创建专属环境
# 默认已经安装好了conda，也已经配置好了国内源

# 使用conda创建ATAC-seq的环境
conda create -n atac -y python=2

# 激活环境
conda activate atac

# 安装所需软件
conda install -y sra-tools
conda install -y trim_galore samtools bedtools
conda install -y deeptools homer meme
conda install -y macs2 bowtie bowtie2 bwa
conda install -y fastqc multiqc
conda install -y sambamba
```

## 数据下载

创建config.sra，内容如下(sra转fastq文件的时候用)：

```shell
2-cell-1 SRR2927015
2-cell-2 SRR2927016
2-cell-5 SRR3545580
2-cell-4 SRR2927018
```

创建srr.list

```shell
SRR2927015
SRR2927016
SRR3545580
SRR2927018
```

下载数据

```shell
source activate atac
mkdir {sra,raw,clean,align,motif,peaks,qc}
cat srr.list |while read id
do
nohup (prefect $id) &
done
# 默认下载目录为~/ncbi/public/sra/
```

*Aspera下载序列可参考——7、使用IBM Aspera Connect下载SRA文件.md*

下载完成后的数据大小如下

```shell
-rwxrwxrwx 1 4.2G Sep 29 09:47 SRR2927015.sra
-rwxrwxrwx 1 5.5G Sep 29 13:02 SRR2927016.sra
-rwxrwxrwx 1 2.0G Sep 28 23:01 SRR2927018.sra
-rwxrwxrwx 1 7.0G Sep 30 06:09 SRR3545580.sra
```

## 第一步、将sra文件转换为

```shell
mv ~/ncbi/public/sra/SRR* sra/
```

创建01_fastq-dump.sh，将一下内容写入进去：

```shell
## 需要用到循环
source activate atac # 激活conda环境
dump=fastq-dump
analysis_dir=raw

# 使用循环在sra转fastq文件的同时，将srr号改为样本名称
cat config.sra| while read id;
do
echo $id
arr=($id)
srr=${arr[1]} # 获取第二列的srr号
sample=${arr[0]} # 获取第一列的sample名
nohup $dump -A $sample -O $analysis_dir --gzip --split-3 sra/$srr.sra &
done
```

## 第二步、fastqc走一波

```shell
nohup fastqc -t 4 -o /qc raw/*gz &
nohup multiqc qc/* & # 合并qc结果
```


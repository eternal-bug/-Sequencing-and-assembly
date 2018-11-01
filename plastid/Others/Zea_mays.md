
# *Zea mays* - [🌽](https://maizegdb.org/)
+ 基因组 - ~2,000Mb
+ 叶绿体 - [NC_001666](https://www.ncbi.nlm.nih.gov/nuccore/NC_001666.2/) - 140384 bp
+ 线粒体 - [AY506529.1](https://www.ncbi.nlm.nih.gov/nuccore/AY506529.1) - 569630 bp

## 细胞器DNA参考序列下载
```bash
# NC_001666
# AY506529.1
```

## 数据来源
+ [PRJNA420919](https://www.ebi.ac.uk/ena/data/view/PRJNA420919) - EMBL下载
+ [PRJNA420919](https://www.ncbi.nlm.nih.gov/bioproject/420919) - NCBI信息

## 项目信息
> we constructed a high-density genetic map using the whole-genome resequencing and specific-locus amplified fragments sequencing (SLAF-seq) techniques for the “G533” and “X224M” elite maize inbred lines, and 196 F2 individuals from a cross between “G533” and “X224M”.

+ [PRJNA420919](https://trace.ncbi.nlm.nih.gov/Traces/study/?acc=PRJNA420919&go=go)

## 下载的文件
+ SRR6360564 - p1
+ SRR6360563 - p2
+ SRR6360403
+ SRR6360390
+ SRR6360385
+ SRR6360370
+ SRR6360363

## 数据下载
```bash
PRJ=PRJNA420919
list=(SRR6360564 SRR6360563 SRR6360403 SRR6360390 SRR6360385 SRR6360370 SRR6360363)
nohup bash ~/Applications/my/download/download_EBI_sequence_data.sh $PRJ ${list[@]} &
```

# *B.oleracea* and *B.rapa*

## 数据来源
+ PRJEB2715
+ [《Use of mRNA-seq to discriminate contributions to the transcriptome from the constituent genomes of the polyploid crop species Brassica napus》](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3428664/)

## 测序文件信息

+ RNA-Seq

| type | No | source | ID | size.bp | coverage |
| --- | --- | --- | --- | --- | --- |
| Brassica napus 1 replicate 1, doubled haploid progeny from B. rapa Ro18 X B.oleracea A12DH cross (B. rapa maternal) | ERR049700 | TGAC
| Brassica napus 1 replicate 2, doubled haploid progeny from B. rapa Ro18 X B.oleracea A12DH cross (B. rapa maternal) | ERR049701 | TGAC
| Brassica napus 1 replicate 3, doubled haploid progeny from B. rapa Ro18 X B.oleracea A12DH cross (B. rapa maternal) | ERR049702 | TGAC
| Brassica napus 1 replicate 4, doubled haploid progeny from B. rapa Ro18 X B.oleracea A12DH cross (B. rapa maternal) | ERR049703 | TGAC
| Brassica napus 2 replicate 1, doubled haploid progeny from B. oleracea A12DH x B. rapa Ro18 cross (B. oleracea maternal) | ERR049704 | TGAC
| Brassica napus 2 replicate 2, doubled haploid progeny from B. oleracea A12DH x B. rapa Ro18 cross (B. oleracea maternal) | ERR049705 | TGAC
| Brassica napus 2 replicate 3, doubled haploid progeny from B. oleracea A12DH x B. rapa Ro18 cross (B. oleracea maternal) | ERR049706 | TGAC
| Brassica napus 2 replicate 4, doubled haploid progeny from B. oleracea A12DH x B. rapa Ro18 cross (B. oleracea maternal) | ERR049707 | TGAC
| B. rapa Ro18 replicate 2 | ERR049708 | TGAC
| B. rapa Ro18 replicate 2 | ERR049709 | TGAC
| B. oleracea A12DH replicate 2 | ERR049710 | TGAC
| B. oleracea A12DH replicate 2 | ERR049711 | TGAC
| Brassica napus 1 replicate 1, doubled haploid progeny from B. rapa Ro18 X B.oleracea A12DH cross (B. rapa maternal) | ERR049712 | TGAC
| Cultivar 'Ceska' | ERR049713 | TGAC
| Aphid resistant rape | ERR049714 | TGAC


## 查看亲本是否为异质的可能
+ 以B.napus的叶绿体序列作为参考序列，查看亲本的测序序列的map情况

### 建立文件链接
```bash
WORKING_DIR=${HOME}/stq/data/anchr/oleracea_and_rapa
cd ${WORKING_DIR}
mkdir ERR049708
mkdir ERR049710
for BASE_NAME in $(ls -d ERR*);
do
  cd ${WORKING_DIR}/${BASE_NAME}
  mkdir 2_illumina
  cd 2_illumina
  ln -fs ../../sequence_data/${BASE_NAME}.fastq.gz ./R1.fq.gz
done
```

### 序列修剪

```bash
for BASE_NAME in $(ls -d ERR*);
do
  cd ${WORKING_DIR}/${BASE_NAME}
  anchr template \
    . \
    --se \
    --basename ${BASE_NAME} \
    --queue mpi \
    --genome 1_000_000 \
    --trim2 "--dedupe --cutoff 4 --cutk 31" \
    --qual2 "25" \
    --len2 "60" \
    --filter "adapter,phix,artifact" \
    --xmx 110g \
    --parallel 24
    
    bsub -q mpi -n 24 -J "${BASE_NAME}" "
      bash 2_trim.sh
    "
done
```

### 建立索引
```bash
~/stq/Applications/biosoft/bwa-0.7.13/bwa index ./genome/*.fa
```

### 比对
```bash

```
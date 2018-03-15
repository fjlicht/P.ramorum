---
title: "Bowtie Usage"
author: "Franz Lichtner"
date: "3/15/2018"
output: html_document
---
# Using Bowtie2 to call SNPs

## Start Pramorum project
### Build index with Bowtie2

```
bowtie2-build -f /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Ref/bowtie2/ramorum1.fasta pramorum1
```

## Use bowtie2 to align corrected reads to reference scaffolds
### Download 'Bless' corrected reads 1 and 2 for each isolate

```
scp *.fastq franzlichtner@129.82.36.76:/data/lichtner/pram/
```

## Start with first isolate
```
bowtie2 -x /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Ref/bowtie2/pramorum1 -1 /Users/Franz/pram1bless23_corr.1.corrected.fastq -2 /Users/Franz/pram1bless23_corr.2.corrected.fastq
```

## Output from Bowtie2 should be .sam file
### Sort samfile
```
samtools view -bS file.sam | samtools sort - file_sorted
```

##
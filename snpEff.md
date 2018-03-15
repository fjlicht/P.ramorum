---
layout: default
title: SnpEff
date: 2017-09-01
---

## Using SNPeff to call some meaningful SNPs between isolates and the reference genome:

### Download SNPeff:

```
wget http://sourceforge.net/projects/snpeff/files/snpEff_latest_core.zip
```

## Call genome of interest from database, this will aid in annotating regions containing SNPs compared to reference genome.
```
java -jar snpEff.jar databases | grep -i phytophthora
```

## Begin executing snpEff to eventually create .csv files to manipulate in R for SNP visualization
```
java -Xmx4g -jar snpEff.jar Phytophthora_ramorum /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Isolates/Bam/multivariants8.vcf > multivariants8.ann.vcf
```

## Should use filtered variant call file containing all genomes
```
java -Xmx4g -jar snpEff.jar Phytophthora_ramorum /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Isolates/Bam/multivariants8_filtered.vcf > multivariants8_filt.ann.vcf
```

## Using individual isolates *108-39* against the reference for SNP id.
```
java -Xmx4g -jar snpEff.jar Phytophthora_ramorum /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Isolates/Bam/108-39_filtered.vcf.gz > 108-39_filt.ann.vcf
```

## Isolate *110_22_filtered.vcf.gz*
```
java -Xmx4g -jar snpEff.jar Phytophthora_ramorum /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Isolates/Bam/110_22_filtered.vcf.gz > 110_22_filt.ann.vcf
```

## Isolate *107_89_filtered.vcf.gz*
```
java -Xmx4g -jar snpEff.jar Phytophthora_ramorum /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Isolates/Bam/107_89_filtered.vcf.gz > 107_89_filt.ann.vcf
```

## *107_72_filtered.vcf.gz*
```
java -Xmx4g -jar snpEff.jar Phytophthora_ramorum /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Isolates/Bam/107_72_filtered.vcf.gz > 107_72_filt.ann.vcf
```

## *pram7_filtered.vcf.gz*
```
java -Xmx4g -jar snpEff.jar Phytophthora_ramorum /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Isolates/Bam/pram7_filtered.vcf.gz > pram7_filt.ann.vcf
```

## *pram6_filtered.vcf.gz*
```
java -Xmx4g -jar snpEff.jar Phytophthora_ramorum /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Isolates/Bam/pram6_filtered.vcf.gz > pram6_filt.ann.vcf
```

## *pram5_filtered.vcf.gz*
```
java -Xmx4g -jar snpEff.jar Phytophthora_ramorum /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Isolates/Bam/pram5_filtered.vcf.gz > pram5_filt.ann.vcf
```

## *pram3_filtered.vcf.gz*
```
java -Xmx4g -jar snpEff.jar Phytophthora_ramorum /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Isolates/Bam/pram3_filtered.vcf.gz > pram3_filt.ann.vcf
```

## *pram1_filtered.vcf.gz*
```
java -Xmx4g -jar snpEff.jar Phytophthora_ramorum /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Isolates/Bam/pram1_filtered.vcf.gz > pram1_filt.ann.vcf
```
##  Here include -csvStats for output to be well curated and manipulatable .csv file *pram4_filtered.vcf.gz*
```
java -Xmx4g -jar snpEff.jar Phytophthora_ramorum -csvStats /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Isolates/Bam/pram4_filtered.vcf.gz >  pram4_filt.ann.vcf
```
## Authors

* **Franz Lichtner** - *Initial work* - [fjlicht](https://github.com/fjlicht)


## License


## Acknowledgments

* http://snpeff.sourceforge.net
* Inspiration
* etc

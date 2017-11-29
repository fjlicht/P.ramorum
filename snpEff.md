---
layout: default
title: SnpEff
date: 2017-09-01
---

#Download SNPeff wget http://sourceforge.net/projects/snpeff/files/snpEff_latest_core.zip
java -jar snpEff.jar databases | grep -i phytophthora

java -Xmx4g -jar snpEff.jar Phytophthora_ramorum /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Isolates/Bam/multivariants8.vcf > multivariants8.ann.vcf
##should use filtered example
java -Xmx4g -jar snpEff.jar Phytophthora_ramorum /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Isolates/Bam/multivariants8_filtered.vcf > multivariants8_filt.ann.vcf

##108-39
java -Xmx4g -jar snpEff.jar Phytophthora_ramorum /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Isolates/Bam/108-39_filtered.vcf.gz > 108-39_filt.ann.vcf

#110_22_filtered.vcf.gz
java -Xmx4g -jar snpEff.jar Phytophthora_ramorum /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Isolates/Bam/110_22_filtered.vcf.gz > 110_22_filt.ann.vcf

#107_89_filtered.vcf.gz
java -Xmx4g -jar snpEff.jar Phytophthora_ramorum /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Isolates/Bam/107_89_filtered.vcf.gz > 107_89_filt.ann.vcf

#107_72_filtered.vcf.gz
java -Xmx4g -jar snpEff.jar Phytophthora_ramorum /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Isolates/Bam/107_72_filtered.vcf.gz > 107_72_filt.ann.vcf

#pram7_filtered.vcf.gz
java -Xmx4g -jar snpEff.jar Phytophthora_ramorum /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Isolates/Bam/pram7_filtered.vcf.gz > pram7_filt.ann.vcf

#pram6_filtered.vcf.gz
java -Xmx4g -jar snpEff.jar Phytophthora_ramorum /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Isolates/Bam/pram6_filtered.vcf.gz > pram6_filt.ann.vcf

#pram5_filtered.vcf.gz
java -Xmx4g -jar snpEff.jar Phytophthora_ramorum /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Isolates/Bam/pram5_filtered.vcf.gz > pram5_filt.ann.vcf

#pram4_filtered.vcf.gz
java -Xmx4g -jar snpEff.jar Phytophthora_ramorum -csvStats /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Isolates/Bam/pram4_filtered.vcf.gz >  pram4_filt.ann.vcf

#pram3_filtered.vcf.gz
java -Xmx4g -jar snpEff.jar Phytophthora_ramorum /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Isolates/Bam/pram3_filtered.vcf.gz > pram3_filt.ann.vcf

#pram1_filtered.vcf.gz
java -Xmx4g -jar snpEff.jar Phytophthora_ramorum /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Isolates/Bam/pram1_filtered.vcf.gz > pram1_filt.ann.vcf

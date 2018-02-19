---
layout: default
title: Bowtie2
date: 2017-10-25
---

##Start Pramorum project over-102517
#build index with bowtie2
bowtie2-build -f /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Ref/bowtie2/ramorum1.fasta pramorum1
##use bowtie2 to align corrected reads to reference scaffolds
#download bless corrected reads 1 and 2 for each isolate
scp *.fastq franzlichtner@129.82.36.76:/data/lichtner/pram/
#Start with pram1
bowtie2 -x /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Ref/bowtie2/pramorum1 -1 /Users/Franz/pram1bless23_corr.1.corrected.fastq -2 /Users/Franz/pram1bless23_corr.2.corrected.fastq

#output from bowtie2 should be sam file
#sort samfile
samtools view -bS file.sam | samtools sort - file_sorted

###Use samtools to sort .bam files then index them before  using mpileup to create vcf 
#new alignment


####taking too long must move to BSPM server
/data/lichtner/pram/ref
/data/lichtner/pram
#Transfer corrected reads from Broderslab1 to BSPM server where I can run bowtie2
scp *.fastq franzlichtner@129.82.36.76:/data/lichtner/pram
##must be in bowtie2 folder to execute
screen -S pram1
./bowtie2 -p 8 -x /data/lichtner/pram/ref/pramorum1 -U /data/lichtner/pram/pram1bless23_corr.1.corrected.fastq -S /data/lichtner/pram/pram1.sam

samtools view -bS pram1.sam > pram1.bam
samtools sort pram1.bam -o pram1.sorted.bam
#stats of bam
samtools flagstat pram1.sorted.bam

samtools mpileup -uf /data/lichtner/pram/ref/ramorum1.fasta pram1.sorted.bam | bcftools view -Ov - > pram1.raw.bcf
bcftools call -c -v pram1.raw.bcf > pram1.variants.vcf
bgzip pram1.variants.vcf
tabix -p vcf pram1.variants.vcf.gz

####pram3
./bowtie2 -p 8 -x /data/lichtner/pram/ref/pramorum1 -U /data/lichtner/pram/pram3bless23_corr.1.corrected.fastq -S /data/lichtner/pram/pram3.sam
27367381 reads; of these:
  27367381 (100.00%) were unpaired; of these:
    2394600 (8.75%) aligned 0 times
    15374889 (56.18%) aligned exactly 1 time
    9597892 (35.07%) aligned >1 times
91.25% overall alignment rate

samtools view -bS pram3.sam > pram3.bam
samtools sort pram3.bam -o pram3.sorted.bam
#stats of bam
samtools flagstat pram3.sorted.bam

samtools mpileup -uf /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Ref/ramorum1.fasta pram3.sorted.bam | bcftools view -Ov - > pram3.raw.bcf
bcftools view pram3.raw.bcf
bcftools call -c -v pram3.raw.bcf > pram3.variants.vcf
bgzip pram3.variants.vcf
tabix -p vcf pram3.variants.vcf.gz

####pram4
#execute in screen pram4
#started 102617 3:38pm finished ~4:15pm
screen -r pram4
./bowtie2 -p 8 -x /data/lichtner/pram/ref/pramorum1 -1 /data/lichtner/pram/pram4bless23_corr.1.corrected.fastq -2 /data/lichtner/pram/pram4bless23_corr.2.corrected.fastq -S /data/lichtner/pram/pram4.sam
##output
23439941 reads; of these:
  23439941 (100.00%) were paired; of these:
    2592817 (11.06%) aligned concordantly 0 times
    13911421 (59.35%) aligned concordantly exactly 1 time
    6935703 (29.59%) aligned concordantly >1 times
    ----
    2592817 pairs aligned concordantly 0 times; of these:
      110260 (4.25%) aligned discordantly 1 time
    ----
    2482557 pairs aligned 0 times concordantly or discordantly; of these:
      4965114 mates make up the pairs; of these:
        4015887 (80.88%) aligned 0 times
        413676 (8.33%) aligned exactly 1 time
        535551 (10.79%) aligned >1 times
91.43% overall alignment rate

samtools view -bS pram4.sam > pram4.bam
samtools sort pram4.bam -o pram4.sorted.bam
#stats of bam
samtools flagstat pram4.sorted.bam

#Franzs-MacBook-Pro:Bam Franz$ samtools flagstat pram4.sorted.bam
#46879882 + 0 in total (QC-passed reads + QC-failed reads)
#0 + 0 secondary
#0 + 0 supplementary
#0 + 0 duplicates
#42863995 + 0 mapped (91.43% : N/A)
#46879882 + 0 paired in sequencing
#23439941 + 0 read1
#23439941 + 0 read2
#41694248 + 0 properly paired (88.94% : N/A)
#42307772 + 0 with itself and mate mapped
#556223 + 0 singletons (1.19% : N/A)
#399776 + 0 with mate mapped to a different chr
#192823 + 0 with mate mapped to a different chr (mapQ>=5)

samtools view pram4.sorted.bam | head -n 5
#must now move .sorted.bam to computer where mpileup is working in samtools. /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Isolates/Bam
#local alternative
export PATH=/usr/local/bin/bin:$PATH
samtools mpileup -uf /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Ref/ramorum1.fasta pram4.sorted.bam | bcftools view -Ov - > pram4.raw.bcf
bcftools view pram4.raw.bcf
bcftools call -c -v pram4.raw.bcf > pram4.variants.vcf
bgzip pram4.variants.vcf
tabix -p vcf pram4.variants.vcf.gz

bcftools filter -O z -o pram4_filtered.vcf.gz -s LOWQUAL -i'%QUAL>20' pram4.variants.vcf.gz
tabix -p vcf pram4_filtered.vcf.gz

####pram5
#execute in screen pram5
#started 102617 4:20pm
screen -S pram5
./bowtie2 -p 8 -x /data/lichtner/pram/ref/pramorum1 -1 /data/lichtner/pram/pram5bless23_corr.1.corrected.fastq -2 /data/lichtner/pram/pram5bless23_corr.2.corrected.fastq -S /data/lichtner/pram/pram5.sam
25200541 reads; of these:
  25200541 (100.00%) were paired; of these:
    3491063 (13.85%) aligned concordantly 0 times
    14488673 (57.49%) aligned concordantly exactly 1 time
    7220805 (28.65%) aligned concordantly >1 times
    ----
    3491063 pairs aligned concordantly 0 times; of these:
      182303 (5.22%) aligned discordantly 1 time
    ----
    3308760 pairs aligned 0 times concordantly or discordantly; of these:
      6617520 mates make up the pairs; of these:
        5403811 (81.66%) aligned 0 times
        520800 (7.87%) aligned exactly 1 time
        692909 (10.47%) aligned >1 times
89.28% overall alignment rate

samtools view -bS pram5.sam > pram5.bam
samtools sort pram5.bam -o pram5.sorted.bam
samtools mpileup -uf /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Ref/ramorum1.fasta pram5.sorted.bam | bcftools view -Ov - > pram5.raw.bcf
bcftools call -c -v pram5.raw.bcf > pram5.variants.vcf
bgzip pram5.variants.vcf
tabix -p vcf pram5.variants.vcf.gz
bcftools filter -O z -o pram5_filtered.vcf.gz -s LOWQUAL -i'%QUAL>20' pram5.variants.vcf.gz
tabix -p vcf pram5_filtered.vcf.gz
####pram6
#execute in screen pram6
#started 110217 1:36pm
screen -S pram6
./bowtie2 -p 8 -x /data/lichtner/pram/ref/pramorum1 -1 /data/lichtner/pram/pram6bless23_corr.1.corrected.fastq -2 /data/lichtner/pram/pram6bless23_corr.2.corrected.fastq -S /data/lichtner/pram/pram6.sam
27877162 reads; of these:
  27877162 (100.00%) were paired; of these:
    4087853 (14.66%) aligned concordantly 0 times
    15871737 (56.93%) aligned concordantly exactly 1 time
    7917572 (28.40%) aligned concordantly >1 times
    ----
    4087853 pairs aligned concordantly 0 times; of these:
      189182 (4.63%) aligned discordantly 1 time
    ----
    3898671 pairs aligned 0 times concordantly or discordantly; of these:
      7797342 mates make up the pairs; of these:
        6469544 (82.97%) aligned 0 times
        575658 (7.38%) aligned exactly 1 time
        752140 (9.65%) aligned >1 times
88.40% overall alignment rate


samtools view -bS pram6.sam > pram6.bam
samtools sort pram6.bam -o pram6.sorted.bam
samtools mpileup -uf /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Ref/ramorum1.fasta pram6.sorted.bam | bcftools view -Ov - > pram6.raw.bcf
bcftools call -c -v pram6.raw.bcf > pram6.variants.vcf
bgzip pram6.variants.vcf
tabix -p vcf pram6.variants.vcf.gz
bcftools filter -O z -o pram6_filtered.vcf.gz -s LOWQUAL -i'%QUAL>20' pram6.variants.vcf.gz
tabix -p vcf pram6_filtered.vcf.gz
####pram7
#execute in screen pram7
#started 10302017
screen -S pram7
./bowtie2 -p 8 -x /data/lichtner/pram/ref/pramorum1 -1 /data/lichtner/pram/pram7bless23_corr.1.corrected.fastq -2 /data/lichtner/pram/pram7bless23_corr.2.corrected.fastq -S /data/lichtner/pram/pram7.sam
31863368 reads; of these:
  31863368 (100.00%) were paired; of these:
    6668073 (20.93%) aligned concordantly 0 times
    16576532 (52.02%) aligned concordantly exactly 1 time
    8618763 (27.05%) aligned concordantly >1 times
    ----
    6668073 pairs aligned concordantly 0 times; of these:
      177150 (2.66%) aligned discordantly 1 time
    ----
    6490923 pairs aligned 0 times concordantly or discordantly; of these:
      12981846 mates make up the pairs; of these:
        11365155 (87.55%) aligned 0 times
        734554 (5.66%) aligned exactly 1 time
        882137 (6.80%) aligned >1 times
82.17% overall alignment rate


samtools view -bS pram7.sam > pram7.bam
samtools sort pram7.bam -o pram7.sorted.bam
samtools mpileup -uf /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Ref/ramorum1.fasta pram7.sorted.bam | bcftools view -Ov - > pram7.raw.bcf
bcftools call -c -v pram7.raw.bcf > pram7.variants.vcf
bgzip pram7.variants.vcf
tabix -p vcf pram7.variants.vcf.gz
bcftools filter -O z -o pram7_filtered.vcf.gz -s LOWQUAL -i'%QUAL>20' pram7.variants.vcf.gz
tabix -p vcf pram7_filtered.vcf.gz
###107-72
#execute in screen 107_72
#started 102717 10:50am
screen -S 107_72
./bowtie2 -p 8 -x /data/lichtner/pram/ref/pramorum1 -1 /data/lichtner/pram/107-72bless23_corr.1.corrected.fastq -2 /data/lichtner/pram/107-72bless23_corr.2.corrected.fastq -S /data/lichtner/pram/107_72.sam
37171338 reads; of these:
  37171338 (100.00%) were paired; of these:
    8228708 (22.14%) aligned concordantly 0 times
    18456291 (49.65%) aligned concordantly exactly 1 time
    10486339 (28.21%) aligned concordantly >1 times
    ----
    8228708 pairs aligned concordantly 0 times; of these:
      3230035 (39.25%) aligned discordantly 1 time
    ----
    4998673 pairs aligned 0 times concordantly or discordantly; of these:
      9997346 mates make up the pairs; of these:
        4246362 (42.47%) aligned 0 times
        1075193 (10.75%) aligned exactly 1 time
        4675791 (46.77%) aligned >1 times
94.29% overall alignment rate
samtools view -bS 107_72.sam > 107_72.bam
samtools sort 107_72.bam -o 107_72.sorted.bam
samtools mpileup -uf /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Ref/ramorum1.fasta 107_72.sorted.bam | bcftools view -Ov - > 107_72.raw.bcf
bcftools call -c -v 107_72.raw.bcf > 107_72.variants.vcf
bgzip 107_72.variants.vcf
tabix -p vcf 107_72.variants.vcf.gz
bcftools filter -O z -o 107_72_filtered.vcf.gz -s LOWQUAL -i'%QUAL>20' 107_72.variants.vcf.gz
tabix -p vcf 107_72_filtered.vcf.gz
###107-89
#execute in screen 107_89
#started 102717 10:50am
screen -S 107_89
./bowtie2 -p 8 -x /data/lichtner/pram/ref/pramorum1 -1 /data/lichtner/pram/107-89bless23_corr.1.corrected.fastq -2 /data/lichtner/pram/107-89bless23_corr.2.corrected.fastq -S /data/lichtner/pram/107_89.sam
samtools view -bS 107_89.sam > 107_89.bam
samtools sort 107_89.bam -o 107_89.sorted.bam

samtools mpileup -uf /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Ref/ramorum1.fasta 107_89.sorted.bam | bcftools view -Ov - > 107_89.raw.bcf
bcftools call -c -v 107_89.raw.bcf > 107_89.variants.vcf
bgzip 107_89.variants.vcf
tabix -p vcf 107_89.variants.vcf.gz
bcftools filter -O z -o 107_89_filtered.vcf.gz -s LOWQUAL -i'%QUAL>20' 107_89.variants.vcf.gz
tabix -p vcf 107_89_filtered.vcf.gz
#110-22
#run in screen -r 107_72
./bowtie2 -p 8 -x /data/lichtner/pram/ref/pramorum1 -1 /data/lichtner/pram/110-22bless23_corr.1.corrected.fastq -2 /data/lichtner/pram/110-22bless23_corr.2.corrected.fastq -S /data/lichtner/pram/110-22.sam

44378056 reads; of these:
  44378056 (100.00%) were paired; of these:
    12363618 (27.86%) aligned concordantly 0 times
    20628876 (46.48%) aligned concordantly exactly 1 time
    11385562 (25.66%) aligned concordantly >1 times
    ----
    12363618 pairs aligned concordantly 0 times; of these:
      4927091 (39.85%) aligned discordantly 1 time
    ----
    7436527 pairs aligned 0 times concordantly or discordantly; of these:
      14873054 mates make up the pairs; of these:
        5945520 (39.98%) aligned 0 times
        1736934 (11.68%) aligned exactly 1 time
        7190600 (48.35%) aligned >1 times
93.30% overall alignment rate
samtools view -bS 110-22.sam > 110_22.bam
samtools sort 110_22.bam -o 110_22.sorted.bam
samtools mpileup -uf /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Ref/ramorum1.fasta 110_22.sorted.bam | bcftools view -Ov - > 110_22.raw.bcf
bcftools call -c -v 110_22.raw.bcf > 110_22.variants.vcf
bgzip 110_22.variants.vcf
tabix -p vcf 110_22.variants.vcf.gz
bcftools filter -O z -o 110_22_filtered.vcf.gz -s LOWQUAL -i'%QUAL>20' 110_22.variants.vcf.gz
tabix -p vcf 110_22_filtered.vcf.gz
#108-39
screen -r pram3
./bowtie2 -p 8 -x /data/lichtner/pram/ref/pramorum1 -1 /data/lichtner/pram/108-39bless23_corr.1.corrected.fastq -2 /data/lichtner/pram/108-39bless23_corr.2.corrected.fastq -S /data/lichtner/pram/108-39.sam

24691096 reads; of these:
  24691096 (100.00%) were paired; of these:
    6909193 (27.98%) aligned concordantly 0 times
    11463418 (46.43%) aligned concordantly exactly 1 time
    6318485 (25.59%) aligned concordantly >1 times
    ----
    6909193 pairs aligned concordantly 0 times; of these:
      2950970 (42.71%) aligned discordantly 1 time
    ----
    3958223 pairs aligned 0 times concordantly or discordantly; of these:
      7916446 mates make up the pairs; of these:
        2643462 (33.39%) aligned 0 times
        966246 (12.21%) aligned exactly 1 time
        4306738 (54.40%) aligned >1 times
94.65% overall alignment rate
samtools view -bS 108-39.sam > 108-39.bam
samtools sort 108-39.bam -o 108-39.sorted.bam
samtools mpileup -uf /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Ref/ramorum1.fasta 108-39.sorted.bam | bcftools view -Ov - > 108-39.raw.bcf
bcftools call -c -v 108-39.raw.bcf > 108-39.variants.vcf
bgzip 108-39.variants.vcf
tabix -p vcf 108-39.variants.vcf.gz
bcftools filter -O z -o 108-39_filtered.vcf.gz -s LOWQUAL -i'%QUAL>20' 108-39.variants.vcf.gz
tabix -p vcf 108-39_filtered.vcf.gz
###
#look at calls- bigger TSTV = stricter
bcftools filter -i'%QUAL>20' variants.vcf.gz | bcftools stats | grep TSTV
#####
##eventually merge all vcf.gz files
##trial here with 3 genomes
bcftools merge pram4.variants.vcf.gz 107_72.variants.vcf.gz pram5.variants.vcf.gz -o multivariants.vcf
bgzip multivariants.vcf
tabix -p vcf multivariants.vcf.gz
##trial here with 8 genomes
bcftools merge pram4.variants.vcf.gz 107_72.variants.vcf.gz pram5.variants.vcf.gz 107_89.variants.vcf.gz 108-39.variants.vcf.gz 110_22.variants.vcf.gz pram7.variants.vcf.gz pram6.variants.vcf.gz -o multivariants8.vcf
bgzip multivariants8.vcf
tabix -p vcf multivariants8.vcf.gz

###FILTER Example
bcftools filter -sLowQual -g3 -G10 \
    -e'%QUAL<10 || (RPB<0.1 && %QUAL<15) || (AC<2 && %QUAL<15) || %MAX(DV)<=3 || %MAX(DV)/%MAX(DP)<=0.3' \
    multivariants8.vcf.gz
    
###Actual filtering step for all variants/SNPs
bcftools stats -F /Users/Franz/Dropbox/P_ramorum/GenomeSeqs/Ref/ramorum1.fasta -s - multivariants8.vcf.gz > multivariants8.vcf.gz.stats
mkdir plots
plot-vcfstats -p plots/ multivariants8.vcf.gz.stats
###
bcftools filter -O z -o multivariants8_filtered.vcf.gz -s LOWQUAL -i'%QUAL>10' multivariants8.vcf.gz
tabix -p vcf multivariants8_filtered.vcf.gz


grep -v "#" multivariants8.vcf.gz | awk '{print $NF}' | awk -F ":" '{print $1}' | awk -F "/" '$1==$2 {print}'
vcftools --gzvcf multivariants8.vcf.gz --extract-FORMAT-info GT | grep "0/1"
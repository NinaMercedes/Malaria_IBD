# Malaria_IBD
This is a repo for IBD analysis tutorial

## Installation
To install create the following conda environment. 
```
conda create -n ibd_tools
conda activate ibdtools
conda install R
conda install plink2
conda install vcftools
## open R
install.packages("remotes")
remotes::install_github("bahlolab/isoRelate")
```
## Input Data
To start you will need your merged and filtered binary multi-sample vcf. You will then need to generate a chromosome list.. see below.
```
bcftools query -f '%CHROM\n your.vcf.gz > chrom_list.txt
awk -i '!x[$0]++' chrom_list.txt > chromosomes.txt
## Open R
chrom <- read.table("chromosomes.txt", header=FALSE)
chrom$V2 <- 1:nrow(chrom)
write.table(chrom, "chrom_map.txt", row.names=FALSE, quote=FALSE, col.names=FALSE)
```

## Make MAP and PED file
These are to input into isoRelate...
```
vcftools --gzvcf POC_only.vcf.gz --plink --chrom-map chrom_map.txt
```
``

# Malaria_IBD
This is a repo for IBD analysis tutorial using isoRelate

## Installation
To install create the following conda environment. 
```
conda create -n ibd_tools
conda activate ibdtools
conda install R
conda install plink2
conda install vcftools
conda install conda-forge::r-dplyr
## open R
devtools::install_github("bahlolab/isoRelate")
install.packages("BiocManager")
BiocManager::install("bahlolab/moimix", build_vignettes = TRUE)

```
## Input Data
To start you will need your merged and filtered binary multi-sample vcf. You will then need to split metadata according to each population of interest. Ignore this step if you have only one population in your vcf already. 
```
Rscript "/mnt/storage13/nbillows/Pop_Gen/master/split_meta2.R" --suffix pf_year --metadata recurated_pf_metadata.tsv --population grouping --wgs_id wgs_id
```

## Make MAP and PED file
These are to input into isoRelate...
```
vcftools --gzvcf POC_only.vcf.gz --plink --chrom-map chrom_map.txt
```
``

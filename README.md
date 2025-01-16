# Malaria_IBD
This is a repo for IBD analysis tutorial using isoRelate

## Preparing files
Let's start by prepping some files. To start you will need your merged and filtered binary multi-sample vcf. You will then need to split metadata according to each population of interest. Ignore this step if you have only one population in your vcf already. 
```
## We will be using the pop_gen conda environment...
conda activate pop_gen
## File prep- making a vcf for each population
Rscript "/mnt/storage13/nbillows/Pop_Gen/master/split_meta2.R" --suffix pf_year --metadata recurated_pf_metadata.tsv --population grouping --wgs_id wgs_id
ls *pf_year.txt > population_files_list.txt
cat population_files_list.txt | xargs -I {} sh -c 'bcftools view -c1 -S {} -Oz --threads 20 -o {}.genotyped.vcf.gz /mnt/storage13/nbillows/Pf_09_24/Pfalciparum_09_24_v2/analysis_09_24_v2/Pf_Nov24_coding_pop_0.001.vcf.gz'
```

## Make MAP and PED file
These are to input into isoRelate...
```
vcftools --gzvcf POC_only.vcf.gz --plink --chrom-map chrom_map.txt
```
``

# PUMAS/PUMA-CUBS
* A tutorial for PUMA-CUBS is coming soon
* Check out our new preprint "Optimizing and benchmarking polygenic risk scores with GWAS summary statistics" [here](https://www.biorxiv.org/content/10.1101/2022.10.26.513833v1).
* Previous version of PUMAS for fine-tuning P+T/C+T PRSs is available [here](https://github.com/qlu-lab/PUMAS/tree/original).

## Input

### Subsampling Input: GWAS summary statisics
The primary input is genome-wide summary statistics in LD-score format. At minimum, this is a flat file with a header row containing the following fields:

| Name | Description  |
|----------------|------------------------------------------------------------------------------|
| SNP | SNP identifier (rsID) |
| A1  | First allele (effect allele)  |
| A2  | Second allele (other allele)  |
| MAF | Minor allele frequency  |
| BETA |  Effect size |
| SE  | Standard error  |    
| P | P-value |   
| N | Sample size |

### Evaluation Input: SNP weights
At minimum, this is a flat file with a header row containing the following fields:

| Name | Description  |
|----------------|------------------------------------------------------------------------------|
| SNP | SNP identifier (rsID) |
| A1  | First allele (effect allele)  |
| A2  | Second allele (other allele)  |
| *weight* |  Name of weights by corresponding tuning parameter and PRS model name|

## PUMAS
* Subsampling
```
LD_PATH = <ld path>

Rscript ./code/PUMAS.subsampling.R \
--k 4 \
--partitions 0.75,0.25 \
--trait_name <trait name> \
--gwas_path <data folder> \
--output_path <output folder>
```
* Evaluation
```
Rscript ./code/PUMAS.evaluation.R \
--k 4 \
--ref_path <LD ref> \
--trait_name <trait name> \
--prs_method lassosum \
--xty_path <subsampling output folder> \
--stats_path <subsampling output folder> \
--weight_path <self-calculated snp weights> \
--output_path <output folder>
```

## PUMA-CUBS
* Subsampling
```
LD_PATH = <ld path>

Rscript ./code/PUMA-CUBS.subsampling.R \
--k 4 \
--partitions 0.6,0.2,0.1,0.1 \
--trait_name <trait name> \
--gwas_path <data folder> \
--output_path <output folder>
```
* Evaluation
```
Rscript ./code/PUMA-CUBS.evaluation.R \
--k 4 \
--ref_path <LD ref> \
--trait_name <trait name> \
--prs_method lassosum \
--xty_path <subsampling output folder> \
--stats_path <subsampling output folder> \
--weight_path <self-calculated snp weights> \
--output_path <output folder>
```

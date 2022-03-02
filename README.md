# sc_rnaseq_10xpipeline
single cell rnaseq for 10x genomics pipeline

## Install Cell Ranger and bcl2fastq
1. Connect to a Linux server by ssh. ex. O2
2. module avil to check available apps and load
module load bcl2fastq/2.20.0.422 cellranger/6.0.0
3. check if loading properly
cellranger --help
bcl2fastq --help
4. create folder yard
mkdir yard
5. perform a test run as decribed in the last section https://support.10xgenomics.com/single-cell-gene-expression/software/pipelines/latest/using/tutorial_in#testrun
cellranger testrun --id=check_install

## convert BCL to fastq
1. follow https://support.10xgenomics.com/single-cell-gene-expression/software/pipelines/latest/using/tutorial_fq to get test BCL data set
2. main code is
cellranger mkfastq --id=tutorial_walk_through \
  --run=/home/cc550/yard/run_cellranger_mkfastq/cellranger-tiny-bcl-1.2.0 \
  --csv=/home/cc550/yard/run_cellranger_mkfastq/cellranger-tiny-bcl-simple-1.2.0.csv
2. Go to final fastq file folder
cd /home/cc550/yard/run_cellranger_mkfastq/tutorial_walk_through/outs/fastq_path/H35KCBCXY/test_sample

## fastq to count
1. follow https://support.10xgenomics.com/single-cell-gene-expression/software/pipelines/latest/using/tutorial_ct
2. get human pbmc fastq files
wget https://cf.10xgenomics.com/samples/cell-exp/3.0.0/pbmc_1k_v3/pbmc_1k_v3_fastqs.tar
tar -zxvf refdata-cellranger-GRCh38-3.0.0.tar.gz
3. get human reference genome
wget https://cf.10xgenomics.com/supp/cell-exp/refdata-gex-GRCh38-2020-A.tar.gz
tar -xzvf refdata-gex-GRCh38-2020-A.tar.gz #using -zxvf will get error messages
4. main code. takes 4 hrs to complete 
srun --pty -p medium -t 00-13:00 --mem=200G cellranger count --id=run_count_1kpbmcs --fastqs=/home/cc550/yard/run_cellranger_count/pbmc_1k_v3_fastqs --transcriptome=/home/cc550/yard/run_cellranger_count/refdata-cellranger-GRCh38-3.0.0
5. go to final output folder <outs>. Data for the Seurat R package locates at outs/filtered_feature_bc_matrix
6. open FileZilla to download outs folder.
host: transfer.rc.hms.harvard.edu
port: 22  (the SFTP port) 
username: your HMS ID (formerly known as eCommons ID), the ID you use to login to O2, in lowercase, e.g., ab123 (not your Harvard ID or Harvard Key) 
password: your HMS ID password, the password you use when logging in to O2

## Seurat
1. open R studio



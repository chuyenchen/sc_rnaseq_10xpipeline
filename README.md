# sc_rnaseq_10xpipeline
single cell rnaseq for 10x genomics pipeline

## Cell Ranger
1. Connect to Linux server by ssh. ex. Argos
2. Download CR following instructions: https://support.10xgenomics.com/single-cell-gene-expression/software/pipelines/latest/using/tutorial_in
3. Add to PATH:
export PATH=/bin:/home/cxc28/yard/apps/cellranger-6.1.2:$PATH

## bcl2fastq
1. Install from source. Download version 2.2(tar) from https://support.illumina.com/sequencing/sequencing_software/bcl2fastq-conversion-software/documentation.html
2. Decompressed in local and upload to HPC:
mkdir bcl2fastq/tmp
scp ~/Documents/Github/bcl2fastq2-v2-20-0-tar/bcl2fastq2-v2.20.0.422-Source.tar.gz cxc28@argos-stgw2.dfci.harvard.edu:/mnt/storage/home/cxc28/bcl2fastq/tmp
export TMP=/home/cxc28/yard/tmp
export SOURCE=${TMP}/bcl2fastq
export BUILD=${TMP}/bcl2fastq2-v2.2.x-build
export INSTALL_DIR=/usr/local/bcl2fastq2-v2.2.x
cd ${TMP} 
3. we should see a file bcl2fastq2-v2.19.x.tar.gz:
tar -xvzf bcl2fastq2-v2.19.x.tar.gz
4. Configure the build:
mkdir ${BUILD}
cd ${BUILD}
chmod ugo+x ${SOURCE}/src/configure
chmod ugo+x ${SOURCE}/src/cmake/bootstrap/installCmake.sh
${SOURCE}/src/configure --prefix=${INSTALL_DIR}
5. Build and install the package:
cd ${BUILD}
make
make install
# assignment
mkdir ~/workdir/assignment
cd ~/workdir/assignment
wget -c ftp://ftp-trace.ncbi.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR879/SRR8797509/SRR8797509.sra  
 sudo apt install sra-toolkit
 # convert sra to one file fastq
fastq-dump --split-spot sample.sra  
 # convert sra to two files fastq
 fastq-dump --split-3 sample.sra
# get unique reads
gzip sample.fastq
zcat sample.fastq.gz | seqkit rmdup -s -o clean.fastq.gz
#[INFO] 471284 duplicated records removed

 


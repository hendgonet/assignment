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
#get 1 unique sample of million read
zcat clean.fastq.gz | seqkit sample -n 1000000 -o sample1_1.fastq.gz
zcat clean.fastq.gz | seqkit sample -n 1000000 -o sample1_2.fastq.gz
zcat clean.fastq.gz | seqkit sample -n 1000000 -o sample1_3.fastq.gz
zcat clean.fastq.gz | seqkit sample -n 1000000 -o sample1_4.fastq.gz
zcat clean.fastq.gz | seqkit sample -n 1000000 -o sample1_5.fastq.gz
#shuffle
seqkit shuffle sample.fastq.gz > shuffled.fastq
gzip shuffled.fastq
zcat shuffled.fastq.gz | seqkit sample -n 1000000 -o sample2_1.fastq.gz
zcat shuffled.fastq.gz | seqkit sample -n 1000000 -o sample2_2.fastq.gz
zcat shuffled.fastq.gz | seqkit sample -n 1000000 -o sample2_3.fastq.gz
zcat shuffled.fastq.gz | seqkit sample -n 1000000 -o sample2_4.fastq.gz
zcat shuffled.fastq.gz | seqkit sample -n 1000000 -o sample2_5.fastq.gz
#use FASTQC to report the difference between S1_1 and S1_2
fastqc -t 1 -f fastq -noextract sample1_1.fastq.gz
#trimming
https://bioinformatics-core-shared-training.github.io/cruk-summer-school-2018/Introduction/SS_DB/Materials/Practicals/Practical1_fastQC_DB.html#checking-read-quality-using-fastqc
cutadapt -m 10 -q 20 -o tp53_r2.fastq_trimmed.fastq.gz tp53_r2.fastq.gz
 


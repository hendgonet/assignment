# assignment
mkdir ~/workdir/assignment
cd ~/workdir/assignment
wget -c ftp://ftp-trace.ncbi.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR879/SRR8797509/SRR8797509.sra  
sudo apt install sra-toolkit
# convert sra to one file fastq
fastq-dump --split-spot sample.sra  
# get 5 samples each one of million reads
gzip sample.fastq
seqkit split sample.fastq.gz -s 1000000
# shuffle
seqkit shuffle sample.fastq.gz > shuffled.fastq
# get 5 shuffled samples each one of million reads
gzip shuffled.fastq
seqkit split shuffled.fastq.gz -s 1000000
# use FASTQC to report the difference between S1_1 and S1_2
fastqc -o ~/home/ngs-01/workdir/assignment --noextract -f fastq sample1_1.fastq.gz
# Mild Trimming for SX_1. {unshuffled}
cutadapt -m 10 -q 20 -o sample1_1_trimmed.fastq.gz sample1_1.fastq.gz
# Aggressive Trimming for SX_2. {shuffled}
cutadapt -m 50 -q 100 -o sample1_2_trimmed.fastq.gz sample1_2.fastq.gz

 


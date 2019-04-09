# assignment
mkdir ~/workdir/assignment
cd ~/workdir/assignment
wget -c ftp://ftp-trace.ncbi.nih.gov/sra/sra-instant/reads/ByRun/sra/SRR/SRR879/SRR8797509/SRR8797509.sra
mv DRR000033.sra sample.sra
sudo apt install sra-toolkit
# convert sra to one file fastq
fastq-dump --split-spot sample.sra  
# get 5 samples each one of million reads
gzip sample.fastq
seqkit split sample.fastq.gz -s 1000000
# shuffle
seqkit shuffle sample.fastq.gz > shuffled.fastq.gz
# get 5 shuffled samples each one of million reads
seqkit split shuffled.fastq.gz -s 1000000
# use FASTQC to report the difference between S1_1 and S1_2
cd shuffled.fastq.gz.split
fastqc  --noexsample.fastq.gz.splittract -f fastq shuffled.part_001.fastq.gz
cd ..
cd sample.fastq.gz.split
fastqc  --noexsample.fastq.gz.splittract -f fastq sample.part_001.fastq.gz
# Mild Trimming for SX_1. {unshuffled}
sudo apt install cutadapt
cutadapt -m 10 -q 20 -o sample1_1_trimmed.fastq.gz sample.part_001.fastq.gz
# Aggressive Trimming for SX_2. {shuffled}
cd ..
cd shuffled.fastq.gz.split
cutadapt -m 50 -q 100 -o sample1_2_trimmed.fastq.gz shuffled.part_001.fastq.gz
# Alignment
cd ..
conda install -c bioconda bwa 
mkdir -p ~/workdir/assignment/bwa_align/bwaIndex
cd ~/workdir/assignment/bwa_align/bwaIndexbwa 
ln -s ~/home/ngs-01/workdir/assignment/chr22_with_ERCC92.fa.
index -a bwtsw chr22_with_ERCC92.fa




 


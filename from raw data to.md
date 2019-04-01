# from raw data sent from sequence centre
1)dowload files: open screen; make a directory; open it; 
```
scp -r ben@graham.computecanada.ca:/home/ben/project/ben/2019_XB_gonad_RNAseq/ .
```
2)FastQC: open screen; open directory with downloaded data; use the commend: 
```
for i in *fastq.gz ; do fastqc $i; done
```
fastqc files with .html prefix will be created in same folder as raw data
3)go to folder where you want to create folder with fastqc.html files, make a directory 'mkdir fastqc_raw' ; dowload files to my googledisk account using command: `scp martin@info.mcmaster.ca:/home/martin/borealis_gonad_transcriptome/data/raw_data/2019_XB_gonad_RNAseq/*fastqc.html .` ; open all html files using `open *`

4)Scynthe

5)Trimmomatic

```
java -jar /home/xue/software/Trimmomatic-0.36/trimmomatic-0.36.jar PE -phred33 -trimlog trim_out.txt /home/martin/borealis_gonad_transcriptome/data/raw_data/2019_XB_gonad_RNAseq/XBO12_R1.fastq.gz /home/martin/borealis_gonad_transcriptome/data/raw_data/2019_XB_gonad_RNAseq/XBO12_R2.fastq.gz /home/martin/borealis_gonad_transcriptome/data/trimm_data/XBO12_R1_paired.fastq.gz /home/martin/borealis_gonad_transcriptome/data/trimm_data/XBO12_R1_single.fastq.gz /home/martin/borealis_gonad_transcriptome/data/trimm_data/XBO12_R2_paired.fastq.gz /home/martin/borealis_gonad_transcriptome/data/trimm_data/XBO12_R2_single.fastq.gz ILLUMINACLIP:/home/xue/Trimmomatic-0.36/adapters/TruSeq2-PE.fa:2:30:10 SLIDINGWINDOW:4:15 MINLEN:36
```

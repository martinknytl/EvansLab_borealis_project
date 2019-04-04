# from raw data sent from sequence centre
**1)dowload files: open screen; make a directory; open it;** 
```
scp -r ben@graham.computecanada.ca:/home/ben/project/ben/2019_XB_gonad_RNAseq/ .
```
**2)FastQC: open screen; open directory with downloaded data; use the command:**
```
for i in *fastq.gz ; do fastqc $i; done
```
fastqc files with .html prefix will be created in same folder as raw data

go to folder where you want to create folder with fastqc.html files, make a directory 'mkdir fastqc_raw' ; dowload files to my googledisk account using command:

```
scp martin@info.mcmaster.ca:/home/martin/borealis_gonad_transcriptome/data/raw_data/2019_XB_gonad_RNAseq/*fastqc.html .` ; open all html files using `open *
```

**4)Scynthe**

`mkdir scynthed_data`
```
for i in *fastq.gz ; do name=$(grep -o "XBO[0-9]*_[A-Z][0-9]" <(echo $i)); /home/xue/software/scythe-master/scythe/2019_XB_gonad_RNAseq -a /home/xue/software/scythe-master/illumina_adapters.fa -p 0.1 $i | gzip > /home/martin/borealis_gonad_transcriptome/data/scynthed_data/$name\_scythe.fastq.gz; done
```

**5)Fastqc

**6)Trimmomatic**

`mkdir trimm_data`

`pwd` /home/martin/borealis_gonad_transcriptome/data/trimm_data

one sample by one

launch screen, open screen, copy follow command:

```
java -jar /usr/local/trimmomatic/trimmomatic-0.36.jar PE -phred33 -trimlog trim_out.txt /home/martin/borealis_gonad_transcriptome/data/raw_data/2019_XB_gonad_RNAseq/XBO8_R1.fastq.gz /home/martin/borealis_gonad_transcriptome/data/raw_data/2019_XB_gonad_RNAseq/XBO8_R2.fastq.gz /home/martin/borealis_gonad_transcriptome/data/trimm_data/XBO8_R1_paired.fastq.gz /home/martin/borealis_gonad_transcriptome/data/trimm_data/XBO8_R1_unpaired.fastq.gz /home/martin/borealis_gonad_transcriptome/data/trimm_data/XBO8_R2_paired.fastq.gz  /home/martin/borealis_gonad_transcriptome/data/trimm_data/XBO8_R2_unpaired.fastq.gz ILLUMINACLIP:/usr/local/trimmomatic/adapters/TruSeq2-PE.fa:2:30:10 SLIDINGWINDOW:4:15 MINLEN:36
```
you can copy next command before the previous one will finish etc. until the last one.

```
java -jar /usr/local/trimmomatic/trimmomatic-0.36.jar PE -phred33 -trimlog trim_out.txt /home/martin/borealis_gonad_transcriptome/data/raw_data/2019_XB_gonad_RNAseq/XBO36_R1.fastq.gz /home/martin/borealis_gonad_transcriptome/data/raw_data/2019_XB_gonad_RNAseq/XBO36_R2.fastq.gz /home/martin/borealis_gonad_transcriptome/data/trimm_data/XBO36_R1_paired.fastq.gz /home/martin/borealis_gonad_transcriptome/data/trimm_data/XBO36_R1_unpaired.fastq.gz /home/martin/borealis_gonad_transcriptome/data/trimm_data/XBO36_R2_paired.fastq.gz  /home/martin/borealis_gonad_transcriptome/data/trimm_data/XBO36_R2_unpaired.fastq.gz ILLUMINACLIP:/usr/local/trimmomatic/adapters/TruSeq2-PE.fa:2:30:10 SLIDINGWINDOW:4:15 MINLEN:36
```
8,12,15,16,17,19,20,21,23,24,26,27,28,29,30,31,32,33,34,35,36

**7)FastQC: open screen; open directory with trimmomatic data (trimm_data); use the command:**
```
for i in *fastq.gz ; do fastqc $i; done
```
fastqc files with .html prefix will be created in folder trimm_data

go to folder where you want to create folder with fastqc.html files in your PC, make a directory 'mkdir fastqc_raw' ; dowload files to e.g. my googledisk account using command:

```
scp martin@info.mcmaster.ca:/home/martin/borealis_gonad_transcriptome/data/raw_data/2019_XB_gonad_RNAseq/*fastqc.html .` ; open all html files using `open *
```


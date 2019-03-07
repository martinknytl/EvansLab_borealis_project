# aaa
1)dowload files: open screen; make a directory; open it; 
```
scp -r ben@graham.computecanada.ca:/home/ben/project/ben/2019_XB_gonad_RNAseq/ .
```
2)FastQC: open screen; open directory with downloaded data; use the commend: 
```
for i in *fastq.gz ; do fastqc $i; done
```
fastqc files with .html prefis will be created in same folder as raw data
3)go to folder where you want to create folder with fastqc.html files, make a directory 'mkdir fastqc_raw' ; dowload files to my googledisk account using command: `scp martin@info.mcmaster.ca:/home/martin/borealis_gonad_transcriptome/data/raw_data/2019_XB_gonad_RNAseq/*fastqc.html .` ; open all html files using `open *`

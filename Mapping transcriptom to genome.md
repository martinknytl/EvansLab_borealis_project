# Mapping transcriptome to genome
Different type of mapping:
- reads (rnaseq read or genomic read) mapping to a genome
- reads mapping to a transcriptome
- gene sequence mapping to a genome
- transcript sequence mapping to a genome

## Mapping transcripts to a genome
Important point to keep in mind when mapping a transcript to a genome:
- genome contain introns, but transcripts are all exons
- to map with splice aware aligner

## Step 1, indexing before mapping
To index the tropicalis genome, you need to download the genome first. The way that you can download the genome is using `wget`.
```
wget ftp://ftp.xenbase.org/pub/Genomics/JGI/Xenla9.2/XL9_2.fa.gz .
```

indexing for GMAP
- the indexing step, the software will take the tropicalis genome and turn it into a format (or sometime it was called a database) that is easier for it to use later. 
```
time gmap_build -g -D /home/martin/laevis_genome -d XLA_indexed /home/martin/laevis_genome/XL9_2.fa.gz
```

## step 2, mapping
To find out how to do mapping, you can consult two resource
- manual: http://research-pub.gene.com/gmap/src/README
- do `gmap --help` on info, which will give you all the options

The way to run it in Graham:
```
#!/bin/bash
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=15
#SBATCH --time=01:20:00
#SBATCH --mem=10G
#SBATCH --job-name=tropicalis_gmap_indexing
#SBATCH --account=def-ben

module load nixpkgs/16.09  gcc/7.3.0
module load gmap-gsnap/2018-07-04
module load samtools/1.9

gmap -D /home/songxy/scratch/tropicalis_transcriptome/tropicalis_genome/db_gmap_tropicalis_v91 -d db_gmap_tropicalis_v91 -A -B 5 -t 15 -f samse /home/songxy/scratch/tropicalis_transcriptome/transcriptome_building/tropicalis_transcriptome_trinityOut.Trinity.SuperTrans.fasta | samtools view -S -b > /home/songxy/scratch/tropicalis_transcriptome/mapping_transcriptome_to_genome/tropicalis_denovoT_tropicalisv91_genome_gmap.bam
```
If you want to run the software on info:
```
gmap -D /home/xue/genome_data/tropicalis_genome/db_tropicalis_gmap -d db_tropicalis_gmap -A -B 5 -t 15 -f samse /home/xue/tropicalis_gonad_transcriptome_Dec2018/data/tropicali_gonad_transcriptome_trinityOut/tropicalis_transcriptome_build_dec2018/tropicalis_transcriptome_trinityOut.Trinity.fasta 
```
- first line of 


## Step 3, read the output file
The detail description of sam (or bam) files are here `https://samtools.github.io/hts-specs/SAMv1.pdf`.
This is how you open a sam or bam file on info. 
```
samtools view tropicalis_denovoT_tropicalisv91_genome_gmap.bam |less -S
```

fff

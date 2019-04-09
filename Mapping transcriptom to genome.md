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
- gmap commands: https://wiki.gacrc.uga.edu/wiki/Gmap

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

imput types:

-D, --dir=directory: to gmap or set the environment variable GMAP database to point to that directory/ path, where the reference indexed genome is

-d, --db=STRING: Genome database

-A, --align: Show alignments

-B, --batch=INT: Batch mode (default = 2)

-t, --nthreads=INT: Number of worker threads

-f, --format=INT: other format for output

outpus files:

-S, --summary: Show summary of alignments only

-b: Output in the BAM format

save as a sam file:
```
gmap -D /home/martin/laevis_genome/XLA_indexed -d XLA_indexed -A -B 5 -t 15 -f samse /home/martin/borealis_gonad_transcriptome/data/trinity_data/borealis_gonad_transcriptome_trinityOut.Trinity.fasta > /home/martin/borealis_gonad_transcriptome/data/gmap/borealis_gmap_output.sam
```

save as a bam file:
```
gmap -D /home/martin/laevis_genome/XLA_indexed -d XLA_indexed -A -B 5 -t 15 -f samse /home/martin/borealis_gonad_transcriptome/data/trinity_data/borealis_gonad_transcriptome_trinityOut.Trinity.fasta | samtools view -S -b > /home/martin/borealis_gonad_transcriptome/data/gmap/borealis_gmap_output.bam
```

- first line of 


## Step 3, read the output file
The detail description of sam (or bam) files are here `https://samtools.github.io/hts-specs/SAMv1.pdf`.
This is how you open a sam or bam file on info. 
```
samtools view tropicalis_denovoT_tropicalisv91_genome_gmap.bam |less -S
```

fff

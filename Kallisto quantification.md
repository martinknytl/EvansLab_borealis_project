https://github.com/griffithlab/rnaseq_tutorial/wiki/Kallisto

https://pachterlab.github.io/kallisto/manual

**1) Kallisto index builds an index from a FASTA formatted file of target sequences. Use trinity output file for indexing.
Builds a kallisto index:**

```
kallisto index --index=borealis_gonad_transcriptome_trinity_index /home/martin/borealis_gonad_transcriptome/data/trinity_data/borealis_gonad_transcriptome_trinityOut.Trinity.fasta
```

Required argument:

- -i, --index=STRING          Filename for the kallisto index to be constructed 

Optional argument:

- -k, --kmer-size=INT         k-mer (odd) length (default: 31, max value: 31)
    --make-unique           Replace repeated target names with unique names
  
The Fasta file supplied can be either in plaintext or gzipped format. Prebuilt indices constructed from Ensembl reference transcriptomes can be download from the kallisto transcriptome indices site.

**2) Kallisto quantification**

Usage: kallisto quant [arguments] FASTQ-files

from trimm_data folder as a current folder (/home/martin/borealis_gonad_transcriptome/data/trimm_data) for individual XBO12:
```
kallisto quant -i /home/martin/borealis_gonad_transcriptome/data/trinity/trinity_data_trimmed/borealis_gonad_transcriptome_trinity_index -o /home/martin/borealis_gonad_transcriptome/data/kallisto /home/martin/borealis_gonad_transcriptome/data/trimm_data/XBO12_R1_paired.fastq.gz /home/martin/borealis_gonad_transcriptome/data/trimm_data/XBO12_R2_paired.fastq.gz 

#do it for all samples (info115 screen kallisto)
for i in /home/martin/borealis_gonad_transcriptome/data/trimm_data/*_R1_paired.fastq.gz; 
    do name=$(grep -o "XBO[0-9]*" <(echo $i)); 
    R1=$name\_R1_paired.fastq.gz; 
    R2=$name\_R2_paired.fastq.gz; 
    kallisto quant  
      -i /home/martin/borealis_gonad_transcriptome/data/trinity/trinity_data_trimmed/borealis_gonad_transcriptome_trinity_index 
      -o /home/martin/borealis_gonad_transcriptome/data/kallisto/$name
      /home/martin/borealis_gonad_transcriptome/data/trimm_data/$R1
      /home/martin/borealis_gonad_transcriptome/data/trimm_data/$R2; 
      done
```

kallisto quant -i /home/martin/borealis_gonad_transcriptome/data/trinity_data/borealis_gonad_transcriptome_trinity_index -o /home/martin/borealis_gonad_transcriptome/data/callisto_quantification XBO12_R1_paired.fastq.gz XBO12_R2_paired.fastq.gz



for i in *_paired.fastq.gz; do name=$(grep -o "XBO[0-9]*_[A-Z][0-9]" <(echo $i)); /home/martin/software/scythe-master/scythe -a /home/martin/software/scythe-master/illumina_adapters.fa -p 0.1 $i | gzip > /home/martin/borealis_gonad_transcriptome/data/scynthed_data/$name\_scythe.fastq.gz; done

Required arguments:

- -i, --index=STRING            Filename for the kallisto index to be used for quantification
                              
- -o, --output-dir=STRING       Directory to write output to

Optional arguments:

-    --bias                    Perform sequence based bias correction
    
- -b, --bootstrap-samples=INT   Number of bootstrap samples (default: 0)

-    --seed=INT                Seed for the bootstrap sampling (default: 42)

-    --plaintext               Output plaintext instead of HDF5
    
-    --fusion                  Search for fusions for Pizzly
    
-    --single                  Quantify single-end reads
    
-    --single-overhang         Include reads where unobserved rest of fragment is predicted to lie outside a transcript
                              
-    --fr-stranded             Strand specific reads, first read forward
    
-    --rf-stranded             Strand specific reads, first read reverse
    
- -l, --fragment-length=DOUBLE  Estimated average fragment length
- -s, --sd=DOUBLE               Estimated standard deviation of fragment length (default: -l, -s values are estimated from paired
                               end data, but are required when using --single)
- -t, --threads=INT             Number of threads to use (default: 1)
-    --pseudobam               Save pseudoalignments to transcriptome to BAM file
-    --genomebam               Project pseudoalignments to genome sorted BAM file
- -g, --gtf                     GTF file for transcriptome information
                              (required for --genomebam)
- -c, --chromosomes             Tab separated file with chromosome names and lengths
                              (optional for --genomebam, but recommended)

Convert BAM to FASTA:

```
java -Xmx2g -jar /usr/local/picard-tools/picard.jar SamToFastq INPUT=borealis_gmap_output.bam FASTQ=borealis_gmap_output.fastq VALIDATION_STRINGENCY=LENIENT
```

Zip the file:

```
gzip borealis_gmap_output.fastq
```

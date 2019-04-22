https://github.com/griffithlab/rnaseq_tutorial/wiki/Kallisto

https://pachterlab.github.io/kallisto/manual

***1) Kallisto index builds an index from a FASTA formatted file of target sequences. Use trinity output file for indexing.
Builds a kallisto index:***

```
kallisto index --index=borealis_gonad_transcriptome_trinity_index /home/martin/borealis_gonad_transcriptome/data/trinity_data/borealis_gonad_transcriptome_trinityOut.Trinity.fasta
```

Required argument:

-i, --index=STRING          Filename for the kallisto index to be constructed 

Optional argument:

-k, --kmer-size=INT         k-mer (odd) length (default: 31, max value: 31)
    --make-unique           Replace repeated target names with unique names
  
The Fasta file supplied can be either in plaintext or gzipped format. Prebuilt indices constructed from Ensembl reference transcriptomes can be download from the kallisto transcriptome indices site.

***2) Kallisto quantification***

Usage: kallisto quant [arguments] FASTQ-files

Required arguments:

-i, --index=STRING            Filename for the kallisto index to be used for
                              quantification
                              
-o, --output-dir=STRING       Directory to write output to

Optional arguments:

    --bias                    Perform sequence based bias correction
    
-b, --bootstrap-samples=INT   Number of bootstrap samples (default: 0)

    --seed=INT                Seed for the bootstrap sampling (default: 42)
    
    --plaintext               Output plaintext instead of HDF5
    
    --fusion                  Search for fusions for Pizzly
    
    --single                  Quantify single-end reads
    
    --single-overhang         Include reads where unobserved rest of fragment is
                              predicted to lie outside a transcript
                              
    --fr-stranded             Strand specific reads, first read forward
    
    --rf-stranded             Strand specific reads, first read reverse
    
-l, --fragment-length=DOUBLE  Estimated average fragment length
-s, --sd=DOUBLE               Estimated standard deviation of fragment length
                              (default: -l, -s values are estimated from paired
                               end data, but are required when using --single)
-t, --threads=INT             Number of threads to use (default: 1)
    --pseudobam               Save pseudoalignments to transcriptome to BAM file
    --genomebam               Project pseudoalignments to genome sorted BAM file
-g, --gtf                     GTF file for transcriptome information
                              (required for --genomebam)
-c, --chromosomes             Tab separated file with chromosome names and lengths
                              (optional for --genomebam, but recommended)

```
kallisto quant --index /home/martin/borealis_gonad_transcriptome/data/gmap/borealis_gmap_output.bam -o /home/martin/borealis_gonad_transcriptome/data/callisto_quantification pairA_1.fastq pairA_2.fastq pairB_1.fastq pairB_2.fastq 
```

Convert BAM to FASTA:

```
java -Xmx2g -jar /usr/local/picard-tools/picard.jar SamToFastq INPUT=borealis_gmap_output.bam FASTQ=borealis_gmap_output.fastq VALIDATION_STRINGENCY=LENIENT
```

Zip the file:

```
gzip borealis_gmap_output.fastq
```

# Ebola mayinga genomic surveillance

Sequence data are used from the DOI: 10.1126/science.1259657 project with PRJNA257197 acceccion number.
The genomic assemly url:
```
https://www.ncbi.nlm.nih.gov/datasets/genome/GCF_000848505.1/
```

First step
Run download to get the data and automatically index it.

```
make download
```

The Makefile is using the SRR1553425 id, but you can swich it for any\ other sample using the SRR variable. For example:
```
make download SRR=SRR1553426
```

Second step
Run fastq for creating reads.
```
make fastq
```

Third step
Run align for creating bam files.
```
make align
```
Fourth step
Run vcf for creating vcf files.
```
make vcf
```

For deleting your directories (bam, refs, reads, vcf) use clean.
```
make clean
```
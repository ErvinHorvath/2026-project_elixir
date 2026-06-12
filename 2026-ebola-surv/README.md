# Ebola mayinga genomic surveillance

The sequence data is used from **DOI: 10.1126/science.1259657** project with **PRJNA257197** acceccion number.\
The genomic assemly url:
```
https://www.ncbi.nlm.nih.gov/datasets/genome/GCF_000848505.1/
```

## Requirments
For running the code successfully you should use wget bwa sra-tools samtools via pixi.\
Run the following:
```
pixi add wget bwa sra-tools samtools
```

## Getting started
**First** step\
Run download to get the data and automatically index it.
```
make download
```

**Second** step\
Run fastq for creating reads.
```
make fastq
```


**Third** step\
Run align for creating bam files.
```
make align
```
**Fourth** step\
Run vcf for creating vcf files.\
The Makefile is using other pipline from the src directory to proceed this task.
```
make vcf
```

For **deleting** the created directories use clean and add the targert folder \(bam, refs, reads, vcf).
```
make clean -rf bam
```

## If you wish to use other samples, parameters
The Makefile is using the **SRR1553425** id, but you can swich it for any other sample using the SRR variable. For example:
```
make download SRR=SRR1553426
```

The Makefile is using **100000** measurements, but you can set your own using the LIMIT variable.
```
make fastq LIMIT=10000
```
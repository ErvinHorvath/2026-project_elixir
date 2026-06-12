# The URL to the genome fasta file.
FASTA_URL=https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/848/505/GCF_000848505.1_ViralProj14703/GCF_000848505.1_ViralProj14703_genomic.fna.gz

# The URL to the annotation.
GFF_URL=https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/848/505/GCF_000848505.1_ViralProj14703/GCF_000848505.1_ViralProj14703_genomic.gff.gz

# The name of the genome file.
GENOME_NAME=ebola-mayinga

# The path to the genome fasta file.
GENOME_FASTA=refs/${GENOME_NAME}.fasta

# The path to the annotation gff file.
GENOME_GFF=refs/${GENOME_NAME}.gff

# The SRR ID of the sample
SRR=SRR1553425

# The name of the sample
SAMPLE=${SRR}

# The name of the alignment BAM file
BAM=bam/${SAMPLE}-${GENOME}.bam

# The number of reads to download. Set to 0 to download all reads.
LIMIT=100000

#The path to the read files.
R1=reads/${SRR}_1.fastq
R2=reads/${SRR}_2.fastq



# No changes below this line, please!

help:
	@echo "Use the source, Luke!"


# make the directories that are needed then download the files and unzip them.
download:
	mkdir -p refs
	wget -O ${GENOME_FASTA}.gz ${FASTA_URL}
	wget -O ${GENOME_GFF}.gz ${GFF_URL}
	gunzip ${GENOME_FASTA}.gz
	gunzip ${GENOME_GFF}.gz
	bwa index ${GENOME_FASTA}

# Use fastq dump to downolad the reads from the SRA, limit to LIMIT
fastq:
	mkdir -p reads
	fastq-dump -X ${LIMIT} --outdir reads --split-files ${SRR}
	

# Align the reads to the genome
align:
	mkdir -p bam
	bwa mem -t 4 ${GENOME_FASTA} ${R1} ${R2} | \
		samtools sort --write-index -o ${BAM}
	samtools flagstat ${BAM}

# Make a vcf file of the variants in the sample
vcf:
	make -f src/run/bcftools.mk \
	REF=${GENOME_FASTA} \
	BAM=${BAM} \
	run


# Remove all the derived files
clean:
	rm -rf bam refs reads vcf

.PHONY: download fastq index align clean vcf
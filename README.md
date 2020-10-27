# 18project_2020

H3mm18 interferes with transcription on H3.3 incorporated chromatin.

We focused on H3mm18 (one of the histone H3.3 subvariants that is expressed in skeletal muscle stem cells) to understand the function of a group that is not incorporated into chromatin.
We performed CEL-Seq2 in C2C12 cells, BRB-seq, ChIL-seq and ATAC-seq in NIH3T3 cells, and BRB-Seq in mouse tissues.


"NIH3T3_Dox" file: NIH3T3 cell line (Dox inducible H3mm18), Mus musculus
"C2C12" file:      C2C12 cell line, Mus musculus
"Mouse_CTX" file:  Tibialis anterior (TA) muscle of 12-week-old H3mm18-/- mice,	Mus musculus


For CEL-Seq2 and BRB-seq, extraction of sample barcodes and unique-molecular-identifiers (UMIs) was performed using UMI-tools (T. S. Smith et al., 2017) (version 1.0.1) with the following commands: umi_tools extract -I r1.fastq --read2-in=r2.fastq --bc-pattern=NNNNNNCCCCCC --read2-stdout for CEL-Seq2, and umi_tools extract -I r1.fastq --read2-in=r2.fastq --bc-pattern= NNNNNNCCCCCCCCC --read2-stdout for BRB-seq.
The reads were trimmed using Cutadapt (M. Martin, 2011)  (version 2.6) wapper, Trim Galore! (version 0.6.6), with the option:  -a GATCGTCGGACT.
The reads were mapped by the aligning software HISAT2 (D. Kim et al., 2015, M. Pertea et al., 2016, D. Kim et al., 2019) (version 2.1.0) to the reference genome (GRCm38, pre-built HISAT2 index, genome_snp_tran). 
Read counts per gene were obtained using featureCounts (Liao Y et al., 2014) (version 2.0.1). Note that UMIs were not used and mitochondrial chromosome genes are excluded in the analysis. 

For ChIL-seq analysis, raw sequencing data were trimmed using Cutadapt (version 2.6) wapper, Trim Galore! (version 0.6.6), with the option:  --2colour 20.
The reads were mapped by the aligning software bowtie2 (B. Langmead et al., 2012) (version 2.3.5.1) to the reference genome (UCSC mm10, Bowtie 2 index), and the uniquely mapped reads were retained.
Mapped data of the same sample were merged by samtools (H. Li, 2009, H. Li, 2011) (version 1.9-170-ge5bac55) with “merge” option. 

For ATAC-seq analysis, raw sequencing data were trimmed using Cutadapt (version 2.6) wapper, Trim Galore! (version 0.6.6), with the options:  --paired --2colour 20.
The reads were mapped by the aligning software bowtie2 (version 2.3.5.1) to the reference genome (UCSC mm10, Bowtie 2 index), and the uniquely mapped reads were retained.

GRCm38/mm10

ChIL-seq signal tracks (bigWig) were generated using  the software deepTools (Ramírez et al., 2016) (version 3.3.0) with the options: bamCoverage --binSize 100 --normalizeUsing CPM --smoothLength 1000.
ATAC-seq signal tracks (bigWig) were generated using  the software deepTools (version 3.3.0) with the options: bamCoverage --centerReads --binSize 100 --normalizeUsing CPM --smoothLength 1000.
We counted reads of ChIL-seq and ATAC-seq within 5kb±TSS regions of the first exon by the software bedtools (version 2.29.2) with “multicov” option.
DESeq2 software (M. I. Love et al., 2014) (1.28.1) was used to calculate normalized counts.

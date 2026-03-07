# De Novo Metagenome Assembly & Annotation

To reconstruct functional genes and larger genomic fragments from our gut microbiome samples, we performed read stitching followed by *de novo* assembly and gene annotation.

## 1. Read Stitching (FLASH)
To increase the effective read length and improve assembly quality, overlapping paired-end reads were merged using **FLASH**.

```bash
# Example command for merging reads (Sample WH1B_089)
flash -o WH1B_089 -z -t 12 -d . \
  ../2-Trimmed/WH1B_089_R1_val_1.fq.gz ../2-Trimmed/WH1B_089_R2_val_2.fq.gz
```
## 2.Metagenomic Assembly (MEGAHIT)

The stitched and uncombined reads were then assembled into contigs using MEGAHIT, an ultra-fast and memory-efficient assembler optimized for complex metagenomes

```bash
# Example command for MEGAHIT assembly
megahit -r ../5-Stitched/WH1B_089.extendedFrags.fastq.gz \
  -1 ../5-Stitched/WH1B_089.notCombined_1.fastq.gz \
  -2 ../5-Stitched/WH1B_089.notCombined_2.fastq.gz \
  -o WH1B_089_asm -t 12

# Run QUAST to evaluate all final contigs simultaneously

quast -o quast_comparison \
  WH1B_089_asm/final.contigs.fa WH1A_090_asm/final.contigs.fa \
  WH2B_091_asm/final.contigs.fa WH2A_092_asm/final.contigs.fa \
  WH3B_093_asm/final.contigs.fa WH3A_094_asm/final.contigs.fa \
  KH1B_101_asm/final.contigs.fa KH1A_102_asm/final.contigs.fa \
  KH2B_103_asm/final.contigs.fa  KH2A_104_asm/final.contigs.fa \
  KH3B_105_asm/final.contigs.fa KH3A_106_asm/final.contigs.fa
```
## 3.QUAST Quality Report

The evaluation generated detailed tabular reports containing key metrics such as Total Length, Number of Contigs, and N50 values for each assembled sample. You can access the raw summary tables below

[View QUAST Text Report](Results/04_Assembly/quast/multiqc_quast.txt)
## 4.Gene Annotation (Prokka)

Following assembly, Prokka was employed to identify and annotate coding sequences (CDS), generating a functional profile for each sample

```bash
# Example command for annotating the assembled contigs
prokka --outdir prokka_WH1B --prefix WH1B WH1B_089_asm/final.contigs.fa --metagenome --cpus 12
```

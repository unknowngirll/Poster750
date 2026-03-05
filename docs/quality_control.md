# Quality Control & Preprocessing

To ensure high-quality downstream analysis, raw FASTQ reads underwent rigorous quality assessment and filtering.

### 1. Initial Assessment
We used **FastQC** to evaluate per-base sequence quality, GC content, and adapter contamination. The results were aggregated using **MultiQC** for a global overview of the 12 samples.

### 2. Trimming and Filtering
Using **TrimGalore** (a wrapper for Cutadapt), we removed low-quality bases (Phred score < 20) and Illumina adapters. 

### Key Findings
* Post-trimming reports show a significant increase in average Phred scores.
* All samples passed the basic quality thresholds for taxonomic classification.

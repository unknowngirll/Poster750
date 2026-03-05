# Quality Control & Preprocessing

To ensure high-quality downstream analysis, raw FASTQ reads underwent rigorous quality assessment and filtering.

## 1. Initial Quality Assessment
First, we used **FastQC** to evaluate the quality of the raw reads, followed by **MultiQC** to aggregate the reports into a single interactive summary.

```bash
# Run FastQC on all reads
fastqc -t 3 -o fastqc_results *.fastq.gz

# Aggregate results using MultiQC
multiqc -o multiqc fastqc_results
```
Results:
The initial assessment revealed the presence of adapter sequences and some drop in base quality towards the end of the reads.
(Note: Click the link above to view the interactive HTML report in your browser)


## 2. Trimming and Filtering
Using TrimGalore, we removed low-quality bases (Phred score < 20) and Illumina adapters.

```
# Example command for trimming sample WH1B_089
trim_galore --paired --quality 20 --stringency 4 \
  ../1-data/R1_fastqc/WH1B_089_R1.fastq.gz \
  ../1-data/R2_fastqc/WH1B_089_R2.fastq.gz
```
Results:
Post-trimming MultiQC reports showed a significant increase in average Phred scores and successful removal of adapters across all 12 samples.

![Sequence Quality After Trimming](../Results/01_Quality_Control/multiqc/Diet-Metagenomics-Study-Korean-vs-Western_multiqc_report_data/fastqc_per_base_sequence_quality_plot.txt)
*(Note: The above plot shows that 100% of our sequences now fall within the 'Green' high-quality zone).*



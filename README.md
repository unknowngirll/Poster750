# Bioinformatics workflow to compare the gut microbiome of Korean and Western diets

## Project Description
This repository contains the scripts, data outputs and visualization reports for our LIFE750 Cycle 1 Team Poster assignment. The project focuses on a bioinformatics workflow to compare the gut microbiome composition of individuals fed Western and Korean diets (specifically focusing on high weight loss samples) using shotgun metagenomics data. Here we perfomed taxonomic profiling of the gut microbiome, biomarker detection and reconstruction of genomic contigs to explore the differences between the gut microbiome of these two diets.

## Objectives
- Characterise and compare the gut microbiome of Korean and Western diets
- Identify potential beneficial gut microbiome changes in both diets

## Background 
The human gut microbiota influences metabolic health, immune function and host physiology, with its composition varying between populations consuming different diets. Advances in metagenomics, which involves sequencing genetic material directly from environmental samples, have enabled comprehensive analysis of microbial communities without the need for culturing. By understanding how different diets alter the gut microbiome, we can begin to understand the role of diet in health outcomes and develop nutritional microbiome research.

## Dataset
The dataset consists of paired-end Illumina sequenced reads from 12 human faecal samples obtained from the EBI Metagenomics database (Study Accession: MGYS00000394 / ERP005558). Samples were collected from 6 participants split equally between those consuming a Western diet (WH) and those consuming a traditional Korean diet (KH), with faecal samples taken both before and after a high weight loss intervention, giving 12 samples in total.

## Bioinformatics Workflow

- **Quality Control of the Raw Reads:** FastQC and MultiQC were used to assess data quality. Sequence histograms showed all reads were high quality and reads had minimal adapter content
- **Trimming:** Adapters (>=4 bases) and low quality bases (quality score < 20) were trimmed with Trim Galore to ensure optimal read quality. As expected, trimming reports indicated minimal adapter removal. FastQC and MultiQC confirmed that high sequence quality was retained 
- **Kraken:** Taxonomic labels were assigned to reads using Kraken to characterise the gut microbiome for both diets
- **Bracken:** The relative abundance of the taxa was estimated using Bracken to explore the composition of the gut microbiome for both diets
- **Visualisation:** Kraken and Bracken reports were visualised using Pavian to compare read taxonomic classification and abundance between populations. Human DNA was removed during analysis.
- **Biomarker Analysis:** LEfSe analysis was used to identify which taxa are responsible for the differences between the diet's microbiomes.
  
- **Stitching Reads:** Reads were stitched together using FLASH to generate larger sequences that facilitate contig assembly
- **MEGAHIT Assembly:** These stitched reads were then assembled into contigs using MEGAHIT, to enable the analysis of longer genomic fragments
- **Quality Control of the Assembly:** the quality of the assembly was assessed with QUAST and the number and length of the contigs were evaluated
- **Genome Binning:** Contig depth was summarised with MetaBAT2. Genome binning was then performed with MetaBAT2 to generate MAGs
- **Quality Control of Bins:** CheckM was used to evaluate bin quality scores, lineage, completeness, and contamination

## Repository Contents
The  `docs` folder contains the following `md` files list the command line inputs, data outputs and key visualisations for each stage of the analysis:
- `quality_control.md`: FASTQC and MULTIQC for raw and trimmed reads
- `taxonomy.md`: Kraken and Bracken analysis
- `biomarkers.md`: LEfSe analysis
- `assembly.md`: FLASH stitching of reads, MEGAHIT assembly and QUAST
  
The `results` folder contains the following files:
- `01_Quality_Control`: FASTQC, MULTIQC, Cutadapt reports
- `02_Taxonomy`: Kraken and Bracken reports and visualisations
- `03_Biomarkers`: LEfSe outputs and visualisations
- `04_Assembly`: Stitching reports, MEGAHIT outputs, QUAST output

## Team Memembers
- Freyja Redmond
- Hannah Kwok
- Nilla Rezaei
- Pimnipa Srisaengsup
- Shaan Basi

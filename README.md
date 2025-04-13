# Bulk RNA-seq Analysis of ATF3 Knockout SMCs

## 📘 Project Description

This project analyzes bulk RNA-seq data from NCBI BioProject [PRJNA716327](https://www.ncbi.nlm.nih.gov/bioproject/?term=PRJNA716327), comparing **ATF3 knockout** vs **control smooth muscle cells (SMCs)**. The goal is to identify differentially expressed genes (DEGs) and perform Gene Ontology (GO) and KEGG enrichment analysis.

## 🧬 Experimental Design

**Comparison Groups:**

- **KO (Knockout):**  
  - SAMN18442667 (SRR14055933)  
  - SAMN18442665 (SRR14055935)

- **Control (WT):**  
  - SAMN18442666 (SRR14055934)  
  - SAMN18442664 (SRR14055936)

## ⚙️ Pipeline Summary

1. **Download FASTQ files** from SRA using `prefetch` + `fasterq-dump`
2. **Quality control** using `FastQC`
3. **Trimming** with `Trimmomatic`
4. **Alignment** to mouse genome (mm10) using `HISAT2`
5. **Quantification** using `featureCounts`
6. **DEG analysis** with `DESeq2` in R
7. **GO and KEGG enrichment** using `clusterProfiler`

## 📁 Directory Structure


## 💻 Dependencies

- [FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/)
- [Trimmomatic](http://www.usadellab.org/cms/?page=trimmomatic)
- [HISAT2](https://daehwankimlab.github.io/hisat2/)
- [SAMtools](http://www.htslib.org/)
- [Subread/featureCounts](https://subread.sourceforge.net/)
- R packages:
  - `DESeq2`
  - `clusterProfiler`
  - `org.Mm.eg.db`
  - `apeglm`

## 📊 Output Highlights

- MA Plot and Volcano Plot of DEGs
- Heatmap of top genes
- GO enrichment (barplot and dotplot)
- KEGG enrichment (no significant pathways found)

## 🔁 How to Reproduce

```bash
# Run from Ubuntu WSL (Linux environment recommended)
cd /mnt/e/UBC_wang_qn1

# Example alignment
hisat2 -p 4 -x /mnt/e/ref_genomes/hisat2_mouse/mm10/genome \
  -1 SRR14055933_1_paired.fastq -2 SRR14055933_2_paired.fastq \
  -S SRR14055933.sam --summary-file SRR14055933_summary.txt

# Run featureCounts, DESeq2, and enrichment steps as shown in R scripts.

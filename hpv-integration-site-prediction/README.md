# HPV Integration Site Prediction

**BIG-TCR Summer Cancer Research Internship — McWilliams School of Biomedical Informatics, UTHealth Houston**

**Researcher:** Jade Winebright  
**Mentors:** Citu Citu, PhD; Zhongming Zhao, PhD

## Project Overview

This research project explored deep-learning methods for predicting whether human DNA sequences represent oncogenic human papillomavirus (HPV) viral integration sites (VISs).

The selected notebooks document the progression from genomic data preparation through sequence filtering and balancing to CNN experiments incorporating both DNA sequence and AlphaGenome-derived epigenetic features.

## Research Workflow

```text
HPV viral integration sites
        ↓
Flank integration coordinates ±500 bp
        ↓
Extract 1,000-bp human-genome sequences
        ↓
Generate non-integration negative regions
        ↓
Filter / deduplicate / balance sequences
        ↓
Explore sequence windows and GC-content effects
        ↓
One-hot encode DNA sequences
        ↓
Combine sequence + AlphaGenome DNase/ATAC inputs
        ↓
CNN classification and evaluation
```

## Data Preparation

The original HPV VIS dataset contained **70,165 integration sites**. Positive sites were flanked by 500 bp upstream and downstream to produce 1,000-bp genomic regions. BEDTools was used to extract corresponding sequences from the human reference genome.

Negative sequences were generated from genomic regions not covered by positive integration sites. Sequences were filtered to valid A/C/G/T bases, and redundancy was reduced using CD-HIT tools at a 90% similarity threshold. The final preprocessing workflow produced **61,082 positive sequences**, with negatives sampled for class balancing.

## Modeling

The research explored convolutional neural networks for genomic-sequence classification. The final included modeling notebook combines one-hot encoded DNA sequence input with AlphaGenome-derived DNase and ATAC features in a multi-input CNN.

The research also investigated GC-content bias and alternative sequence-window approaches.

## Reported Results

According to the final research poster:

- Initial CNN: ROC AUC approximately **0.52**, PR AUC approximately **0.52**
- After filtering GC-content extremes: ROC AUC **0.65**, PR AUC **0.72**
- CNN incorporating AlphaGenome DNase/ATAC features: ROC AUC **0.76**, PR AUC **0.65**

The project identified limited validation generalization and signs of overfitting as important limitations.

## Repository Structure

```text
hpv-integration-site-prediction/
├── README.md
├── .gitignore
├── requirements.txt
├── code/
│   ├── 01_vis_sequence_extraction.ipynb
│   ├── 02_negative_sequence_generation.ipynb
│   ├── 03_dataset_balancing.ipynb
│   ├── 04_kmers_and_windows.ipynb
│   └── 05_cnn_alphagenome.ipynb
└── poster/
    └── BIG_TCR_HPV_Integration_Poster.pdf
```

## Notebook Guide

**01 — VIS Sequence Extraction**  
Prepares positive HPV integration-site coordinates, creates ±500-bp flanking regions, and extracts genomic sequences.

**02 — Negative Sequence Generation**  
Builds candidate non-integration regions and extracts negative genomic sequences while avoiding positive VIS regions.

**03 — Dataset Balancing**  
Explores positive/negative datasets, sampling, binary labels, class balancing, and sequence characteristics.

**04 — k-mers and Windows**  
Experiments with sequence windows/k-mer-oriented preprocessing and sequence-classification approaches.

**05 — CNN + AlphaGenome**  
Combines one-hot DNA sequence data with AlphaGenome-derived DNase/ATAC matrices in a multi-input CNN and evaluates the classifier.

## Code Notes

Because the notebooks were developed in a research computing environment, some cells may contain original environment-specific paths, package-installation commands, intermediate experimentation, or references to data files that are not included here.

## Data Availability

The underlying genomic datasets and large intermediate files are not included in this portfolio repository. This package is intended to demonstrate the code and methodology developed during the internship, accompanied by the final research poster.

## Limitations and Future Work

The final poster notes that the CNN models showed limited generalization beyond the training set and signs of overfitting. Future work proposed additional model optimization, larger datasets, and investigation of transformer-based genomic models.

## Acknowledgement

This work was completed as part of the Biomedical Informatics, Genomics and Translational Cancer Research Training Program (BIG-TCR), funded by the Cancer Prevention & Research Institute of Texas (CPRIT RP210045).

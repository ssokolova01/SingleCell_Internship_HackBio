# SingleCell_Internship_HackBio
# Project Stage 2: Single-Cell RNA-Seq Analysis of Bone Marrow Sample Using Standard Scanpy Workflow




<img width="482" height="388" alt="image" src="https://github.com/user-attachments/assets/48474d39-1d06-4d43-b99a-bbe77ff6b64d" />

<img width="482" height="388" alt="image" src="https://github.com/user-attachments/assets/7cb44232-56fe-416b-8c04-5154ae89e743" />



## **Objective:** Sample origin identification and biological interpretation of cell types found in the single-cell dataset.

## Workflow

**0. Tools And Dataset Preparation** - Packages and libaries installation, Loading and exploring dataset structure

*Installation*

!pip install scanpy

!pip install anndata

!pip3 install igraph

!pip install celltypist

!pip install decoupler

!pip install fa2-modified

import scanpy as sc

import anndata as ad

import decoupler as dc

import pandas as pd

import seaborn as sns

*Data import*

.h5_ad file

**1. Pre-processing** - Quality control & Normalization

- Remove duplicate gene names;

- Assess cell  quality metrics (genes & UMI counts per cell, mitochondrial (MT), ribosomal (RIBO), hemoglobin (HB) gene content);
Filtering thresholds: MT < 5%, RB < 10%, and HB < 5%

- Filtering was not performed due to minimal contamination (MT genes < 2%; RIBO genes < 5%; no HB genes detected);

- Remove doublets using scrublet.
   
2. **Cell Population Analysis** - PCA, Leiden clustering, UMAP
   
3. **Annotation** - Cell type identification, UMAP visualization of annotated cells




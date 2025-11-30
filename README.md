# SingleCell_Internship_HackBio
# Project Stage 2: Single-Cell RNA-Seq Analysis of Bone Marrow Sample Using Standard Scanpy Workflow




<img width="482" height="388" alt="image" src="https://github.com/user-attachments/assets/48474d39-1d06-4d43-b99a-bbe77ff6b64d" />

<img width="482" height="388" alt="image" src="https://github.com/user-attachments/assets/7cb44232-56fe-416b-8c04-5154ae89e743" />



## **Objective:** Sample origin identification and biological interpretation of cell types found in the single-cell dataset.

## Workflow

**0. Tools And Dataset Preparation** - Packages and Libaries Installation & Loading and Exploring Dataset Structure

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

**1. Pre-processing** - Quality Control & Normalization

*Quality Control*

- Remove duplicate gene names;

- Assess cell  quality metrics (genes & UMI counts per cell, mitochondrial (MT), ribosomal (RIBO), hemoglobin (HB) gene content);
      Filtering thresholds: MT < 5%, RB < 10%, and HB < 5%

- Filtering was not performed due to minimal contamination (MT genes < 2%; RIBO genes < 5%; no HB genes detected);

- Remove doublets using scrublet.

*Normalization*

- Standardize expression;

- Select highly variable genes (top 1000 genes were selected).
   
2. **Cell Population Analysis** - Dimensionality Reduction & Clustering

*Dimensionality Reduction*

- PCA reduction of gene expression space.

*Clustering*

- Building cell neighborhood graph;

- Leiden clustering of cell populations by similar expression profiles; 

- UMAP 2D visualization.
   
3. **Annotation** - Cell Type Identification & UMAP Visualization of Annotated Cells

- Gene set enrichment analysis using canonical markers retrieved from PanglaoDB database; 

- Matching clusters to known cell types using decoupler;

- Visualization of annotated clusters on UMAP.

## **Findings**

*8 unique clusters have been identified.*

List of the annotated clusters:

Neutrophils, Gamma delta T cells (γδ T Lymphocytes), Nuocytes (Type 2 Innate Lymphoid Cells, ILC2), Natural Killer (NK) cells, B cells naïve, Platelets, Plasma cells, Monocytes.

*Neutrophils*: white blood cell, provides immune response to infection within phagocytosis; boost response of other immune cells.

*Gamma delta T cells*: a unique and less abundant subset of T cells in peripheral blood; vital to the initial inflammatory and immune responses; bridge innate and adaptive immunity. Can be present in bone marrow.

*Nuocytes*: defends against parasitic worms and contributes to allergic responses (inflammation); involved in tissue repair and remodelling; enriched in mucosal organs, (lungs and intestines), lymphoid organs (spleen and mesenteric lymph nodes).

*Natural Killer (NK) cells*: kill virus-infected cells and cancer cells without prior activation; destroy target cells releasing perforins and granzymes. Develop and mature in bone marrow, mature are in bloodstream and other, mostly lymphoid, organs.

*B cells naïve*: mature B cells unfamiliar with antigen; undergo positive and negative selection processes in bone marrow and spleen to distinguish antigens form self-tissues; migrate to spleen and lymph nodes after maturation; can be found in the blood. 

*Platelets*: cell fragments from megakaryocyte circulating in blood; responsible for clotting and wound healing; promote tissue regeneration.

*Plasma cells*: white blood cells that develop from activated B lymphocytes (B cells); responsible for producing antibodies.

*Monocytes*: the largest white blood cells; detect and respond to pathogens, involved in inflammation, tissue repair and maintain balance of the immune system; transform into macrophages and dendritic cells when migrate in tissues.

## **Biological Interpretation**

**The set of the found cell clusters corresponds to peripheral blood (leukocyte-enriched fraction).**

Reasons to reject bone marrow origin of sequenced sample.

Bone marrow of the healthy adult contains blood-forming hematopoietic stem cells (HSC) and structural mesenchymal stem cells (MSC) lineage populations. From MSC develop stromal lineages including mesenchymal stromal cells, osteoblasts (bone-forming cells), and adipocytes (fat cells). Principal cell lineages of the bone marrow are myeloid and lymphoid lineages, which starts from the myeloid and lymphoid progenitor cells. Common myeloid progenitor cell then proceeds into megakaryocytic, erythroid and myeloid lineages which start from megakaryocyte-erythrocyte progenitor cell and granulocyte-monocyte progenitor cell. Common lymphoid progenitor is responsible for all the lymphoid lineage cells from lymphoblast to lymphocytes and NK cells. Lineages start from blast stage, then they progress in differentiation, and their names depend on cell line. 

There are no Hematopoietic Stem and Progenitor Cells (HSPCs) clusters or immature blood cells (e.g., myeloblasts, lymphoblasts, megakaryocytes, erythroblasts, reticulocytes) found in the analysed sample. Detection of stem cells, progenitors and immature forms in the sample would be a strong indicator of its bone marrow origine. In opposite, all found cell types are mature and highly differentiated, even though some of them could be found in the bone marrow in certain stages and conditions. Also, no non-hematopoietic stromal cells of supporting microenvironment were detected. 

Distribution of the healthy bone marrow usually represents the abundance of the neutrophilic cell lineage, including immature forms such as promyelocytes, myelocytes and neutrophils; there is also a high level of erythroblasts; lymphocytes are present in smaller quantities. Thus, the distribution of cells in the studied sample differs from the typical cell distribution in bone marrow. 

The identified cell type which is the most atypical for bone marrow is nuocytes, especially regarding their high level in the studied sample.

## **Conclusion**

***Reference context.*** Apart from erythrocytes (red blood cells), the typical peripheral blood contains leukocytes (neutrophils, lymphocytes, monocytes, eosinophils, basophils) and thrombocytes (platelets). 
Eosinophils and basophils have very low level or can be absent. Neutrophils, lymphocytes, monocytes and platelets are essential. In healthy adult human blood, neutrophils prevail over lymphocytes, and platelets prevail over white blood cells. 

***Single cell analysis insights.***

***Cluster proportions and Cell type deviations.*** According to the cluster proportions, the most abundant identified cell types are Gamma delta T cells, Natural Killers cells (NK cells) and Nuocytes. The least represented is platelets cluster. Overall, the most represented cells belong to lymphocytes (Gamma delta T cells, NK cells, B cells naïve and plasma cells) and nuocytes also have lymphoid origin. Thus, clusters of the lymphoid lineage cells predominate in number and are highly populated.

***Cell type deviations.*** Cell type proportion is altered. There is a lymphocytes expansion. Neutrophils are dramatically lower represented than lymphocytes. High level of non-bloodstream-typical cell clusters (nuocytes, NK cells, gamma delta T cells, plasma cells) appears. Both B naïve cells and plasma cells occurrence can indirectly indicate high antigen level (e.g., pathogen) and the need to produce a lot of antibodies. 

Given their unique nature as anucleate cell fragments, the low occurrence of platelets is difficult to interpret based solely on the clustering results.

***Functional state.*** Immune system activation. Inflammation, most likely infectious nature. Expression of CCL genes coding chemokines and IL genes coding cytokines, which are the markers of an active infection inflammation process. 

***Conclusion.*** Cell cluster qualitative and quantitative distribution presents peripheral blood in activated immune system status and acute intense inflammation process, most probably caused by infection. Further functional gene analysis is required to clarify the nature of the pathology.


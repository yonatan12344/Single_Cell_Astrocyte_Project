# Single_Cell_Astrocyte_Project
* The data in this project is taken from the following paper, "Disease-associated astrocytes in Alzheimer’s disease and aging".
The count matrix file I used called GSE143758_Admouse_Hippocampus_7m_AllNuclei_UMIcounts.txt is from the Disease-associated astrocytes in 
Alzheimer’s disease and aging paper (PMID:32341542). The GEO accession ID  for the dataset is GSE143758. 

* Disclaimer
This project is purely an exercise in learning bioinformatics, and its results should not be taken as biologically valid, as several steps, such as doublet detection, figuring out whether Sctransform or the NormalizeData-ScaleData-FindVariableFeatures was better suited to the data was not performed. I also did not look into what the normal range of mitochondrial expression for astrocytes is.

* Background: snRNA seq is an approach that allows you to understand the expression of cells by looking at their
nucleus. Typically, snRNA seq data is analyzed very similarly to scRNA seq data, although it is important to note
that you are primarily going to be looking at transcripts from the nucleus and, in theory,
should have fewer mitochondrial reads in the data. It is a very good idea to look at the localization of the transcripts
you are studying as well as the mitochondrial content of the cells you are studying to be better informed during your QC 
steps. The samples here come from 7-month-old male mice who are WT or 5xFAD mice, which are intended to simulate AD

* Identifying astrocytes and exporting their cells for further pseudobulk analysis was done in the Clean_Analysis.RMD file, while pseudobulk analysis of the astrocyte cells only was done in the true_astrocyte_analysis.RMD file.

* Workflow:
1. QC and normalization of snRNA seq data, importantly, snRNA seq data should have
lower mitochondrial content than scRNA seq data, so my 5 percent cutoff may have been
too high. QC metrics will be a bit different and determined by examining plots for each batch 
separately.

2. ScTransform was used for normalization, although I am unsure as to whether this
approach is a better fit for my data than traditional normalization, scaling, and finding variable
features methods. 

3. Used an elbowplot to determine the ideal number of dimensions for PCA and UMAP.
Then, I created PCA and UMAP plots to examine the potential influence of batch effects on the data.

4. This is a redundant step that was not really used, but I ran PrepSCTmarkers on the Seurat
object in order to deal with the fact that I have separate batches to work with, and then ran Findall markers
to isolate potential marker genes for each of the clusters, which in theory should correspond
to separate cell types.

5. I just visualized the distribution of some transcripts that the paper mentioned were used to identify astrocytes
as well as AQP4 on the Seurat clusters, to identify which clusters likely contain the astrocytes.

6. 1. Took the astrocyte clusters and saved them as a Seurat object and exported them as
a count matrix csv file.

**PSEUDOBULK STEPS**

1. I did some preprocessing checks, but ultimately did not modify the data since I chose to rely on the
QC was already performed on the entire scRNA seq dataset. I subsetted the astrocyte data from
earlier.

2. I did some object manipulation to get sample states (AD vs WT) organized within the Seurat object
clearly.

3. I normalized the data, identified variable features, and scaled them.

4. I looked for batch effects with PCA, and used an ElbowPlot to find the ideal
number of dimensions for running UMAP later on.

5. After I ran Findneighbors and FindClusters, I ran UMAP.

6. I visualized the UMAP with respect to. AD and WT, and also displayed it with respect
to batches.

7. I did differential gene expression testing with DESEQ2 after performing pseudobulking

8. I visualized the DESEQ2 results with an ma and volcano plot.

* Results and Figures
# QC PLOTS for entire ~57 k cell dataset which includes more than Astrocytes
<img width="514" height="317" alt="image" src="https://github.com/user-attachments/assets/f0c2f750-d659-45c5-af97-7dff1a5f523c" />
<img width="514" height="317" alt="image" src="https://github.com/user-attachments/assets/16c52470-b59e-4af3-be8b-a5918031ca19" />
<img width="514" height="317" alt="image" src="https://github.com/user-attachments/assets/1a2e590c-2964-4ec3-9574-49499a7f86c0" />
<img width="514" height="317" alt="image" src="https://github.com/user-attachments/assets/58270ee7-46d2-4f5a-aa89-aacd151170be" />
<img width="514" height="317" alt="image" src="https://github.com/user-attachments/assets/e4d4ceaa-cbef-40b0-b00b-6ccf48868db7" />

# Batch Effects in 57k data
<img width="514" height="317" alt="image" src="https://github.com/user-attachments/assets/45311569-cad6-4df0-9d5a-84db1290b707" />

* Unannotated Cell Types
* <img width="514" height="317" alt="image" src="https://github.com/user-attachments/assets/490fadc0-75ff-4393-b98f-8f54ad68be2a" />

Visulazing the distribution of some transcripts to find clusters corresponding to astrocytes
<img width="1181" height="647" alt="image" src="https://github.com/user-attachments/assets/e3713e6a-9371-4319-a7cc-676498bdf1ab" />

Astrocytes vs Nonastrocyte clusters
<img width="700" height="432" alt="image" src="https://github.com/user-attachments/assets/21f87580-c27c-4351-8037-c0c1f9233471" />


# ASTROCYTE SPECIFIC QC CHECKS
<img width="514" height="317" alt="image" src="https://github.com/user-attachments/assets/3690c14a-4fd2-45f5-8e37-f2d1e4f7146a" />
<img width="514" height="317" alt="image" src="https://github.com/user-attachments/assets/7aa27baa-5244-40a3-b87f-54feb87e6670" />
<img width="514" height="317" alt="image" src="https://github.com/user-attachments/assets/844896ca-4d3d-497c-82f8-369f3a205ad6" />

* Variable Features for Astrocytes
<img width="514" height="317" alt="image" src="https://github.com/user-attachments/assets/4efad940-9264-4b05-8997-bd52a7e61622" />

* Checking for Batch Effects in Astrocytes with PCA and UMAP
<img width="514" height="317" alt="image" src="https://github.com/user-attachments/assets/28fc5ee9-74ad-47d0-a9bd-417c1ba57c08" />
<img width="514" height="317" alt="image" src="https://github.com/user-attachments/assets/0daf4cf5-d017-479d-9eca-d4cc1d3e2dfd" />

* Visualizing UMAP comparing AD to WT
<img width="514" height="317" alt="image" src="https://github.com/user-attachments/assets/279e53c0-3ca6-48ea-8421-22f22ba225d7" />

* MA PLOT and VOLCANO PLOT
Significance line for volcano plot is the default value of the EnhancedVolcano function; the significance of each gene may be different.

<img width="514" height="317" alt="image" src="https://github.com/user-attachments/assets/9f4b047f-36bb-4c79-86a8-264ef1970435" />

<img width="700" height="432" alt="image" src="https://github.com/user-attachments/assets/f4c6ae9e-9c9a-4d6e-95d4-df4185b8ed87" />

* Results for AQP4 expression
<img width="534" height="132" alt="image" src="https://github.com/user-attachments/assets/994e6f2e-4393-482a-ae9d-39e9426ccd97" />







Conclusions, I don’t think there are super strong batch effects in the data, and AQP4 expression does not seem to differ between AD and WT mice. This
could be because AQP4 is not really expressed much at the nucleus, poor sample size, or there genuinely not being a difference in AQP4 expression when comparing
WT to AD mice.


# Single_Cell_Astrocyte_Project
* The data in this project is taken from the following paper, "Disease-associated astrocytes in Alzheimer’s disease and aging".
The count matrix file I used called GSE143758_Admouse_Hippocampus_7m_AllNuclei_UMIcounts.txt is from the Disease-associated astrocytes in 
Alzheimer’s disease and aging paper (PMID:32341542). The GEO asscession id for the dataset is GSE143758. 

* Disclaimer
This project is purely an excersise in learning bioinformatics, and its results should not be taken as biologically valid,
as several steps such as doublet detection, figuring out whether Sctransform or the NormalizeData-ScaleData-FindVariableFeatures
approach was better suited to the dataset. I also did not look into what the normal range of mitochondrial expression for astrocytes
are. 

* Background: snRNA seq is an approach that allows you to understand the expression of cells by looking at their
nucleus. Typically snRNA seq data is analyzed very simmilarly to scRNA seq data, although it is important to note
that your are primarily going to be looking at transcripts from the nucleus and in theory
should have less mitochondrial reads in the data. It is a very good idea to look at the localization of the transcripts
you are studying as well as the mitochondrial conent of the cells you are studying to be better informed during your QC 
steps.

* Workflow:
1. QC and normalization of snRNA seq data, importantly snRNA seq data should have
lower mitochondrial content then scRNA seq data, so my 5 percent cutoff may have been
to high. QC metrics will a bit different and determined by examing plots for each batch 
separately.

2. ScTransform was used for normalization, although I am unsure as to whether this
approach is a better fit for my data than traditional normalization, scaling, and finding variable
features methods. 

3. Used an elbowplot to determine the ideal number of dimensions for PCA and UMAP.
Then made PCA and UMAP plots, to see the potential influence of batch effects on the data.

4. This is a redundant step that was not really used, but I ran PrepSCTmarkers on the seurat
object in order to deal with the fact I have seperate batches to work with, and then ran Findall markers
to isolate potential marker genes for each of the clusters, which in theory should correspond
to separate cell types.

5. I just visualized the distribution of some transcripts the paper mentioned that were used to identify astrocytes
as well as AQP4 on the seurat clusters, to identify which clusters likely contain the astrocytes.

6. Took the astrocyte clusters and saved them as a seurat object and exported them as 
a count matrix csv file.

**PSEUDOBULK STEPS**

1. I did some preprocessing checks, but ultimately did not modify the data since, choosing to rely on the
QC was already performed on the entire scRNA seq dataset I subseted the astrocyte data from
earlier.

2. I did some object manipulation to get sample states (AD vs WT) organized within the seurat object
clearly.

3. I normalized the data, found variable features, and scaled it.

4. I looked for batch effects with PCA, and used and ElbowPlot to find the ideal
number of dimension for running UMAP later on.

5. After I ran Find neighbors and Find Clusters, I ran UMAP

6. I visualized the UMAP with respect to. AD and WT, and also displayed it with respect
to batches.

7. I did differntial gene expression testing with DESEQ2 after performing pseudobulking

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









I don't think there is a super strong batch effect in the data, based of the UMAP
and PCA plots. Also AQP4 expression did not seem to vary much between AD and WT
mouse populations.



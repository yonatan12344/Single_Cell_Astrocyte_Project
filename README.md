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
that it shou

* Workflow:
1. QC and normalization of snRNA seq data, importantly snRNA seq data should have
lower mitochondrial content then scRNA seq data, so my 5 percent cutoff may have been
to high. QC metrics will a bit different and determined by examing plots for each batch 
seprately.

2. ScTransform was used for normalization, although I am unsure as to whether this
approach is a better fit for my data than traditional normalization, scaling, and finding variable
features methods. 

3. Used an elbowplot to determine the ideal number of dimensions for PCA and UMAP.
Then made PCA and UMAP plots, to see the potential influence of batch effects on the data.

4. This is a redudant step that was not really used, but I ran PrepSCTmarkers on the seurat
object in order to deal with the fact I have seperate batches to work with, and then ran Findall markers
to isolate potential marker genes for each of the clusters, which in theory should correspond
to seperate cell types.

5. I just visualized some genes the paper mentioned 


* Results and Figures

I don't think there is a super strong batch effect in the data, based of the UMAP
and PCA plots. Also AQP4 expression did not seem to vary much between AD and WT
mouse populations.



RAVED - Reproducible Analysis and Validation of Expression Data
======

Authors: Mengyuan Kan, Maya Shumyatcher, Blanca Himes

## Introduction

RAVED is a pipeline written in two R Markdown scripts initially developed for reproducible analysis of microarray dataset from GEO, including the following:
* Raw intensity data download
* Phenotype file preparation
* Quality control (QC) and outlier detection
* Comparison assignment
* Differential expression (DE) analysis 

Several freely accessible R packages for microarray data analysis are used in this pipeline. We use GEO dataset GSE4917 as an example and provide two R Markdown templates to reproduec the analysis pipeline and reports for GSE4917. The template_QC_report.Rmd script goes first including the steps of raw data download, phenotype file preparation, and QC. The template_DE_analysis_report.Rmd takes the output from the template_QC_report.Rmd and performs the DE analysis of the comparison of interest. The RMD files and HTML reports for other microarray data used for our integrative analysis of transcriptomic data asthma and glucocorticoid response can be found in the folder microarray.

Prerequisite R packages for microarray data analysis include:
* Data download: GEOquery
* Raw data processing: oligo and affy
* Statistical analysis for outlier detection: Hmisc
* DE analysis: limma
* Batch effect adjustment: sva
* Microarry data gene annotation: annotation, hgu133plus2.db and hugene10sttranscriptcluster.db

## Pipeline description

### Data download
Raw data are downloaded from GEO directly including GSEMatrix files that are used for phenotype file preparation, and raw intensity data .CEL files, if provided, that are used for QC and DE analysis.

### Phenotype file preparation
Raw phenotype data derived from GSEMatrix files is first overviewed and then manually modified to a more informative and concise phenotype file with the columns GEO_ID, Subject, Disease, Treatment, Age, Gender, etc

### QC and outlier detection

The following QC metrics are included in a routine analysis. QC steps of which metrics are used for outlier detection are marked with an asterisk.
* Boxplots and density plots for raw probe intensities*
* RNA degradation plots
* Density plots for perfect match (PM) and mismatch (MM) probe
* MA plots*
* Spatial plots*
* Boxplots for the normalized unscaled standard error (NUSE) and relative log expression (RLE)*
* Heatmap and dendrogram for distance between arrays*
* Principal component analysis (PCA) plots

A hard filter is applied to determine the outliers to remove: a sample which is designated an outlier by more than two methods will be excluded from DE analysis. A column showing whether the sample passes QC is added to the phenotype file. We suggest researchers manually inspect the QC metrics and plots to identify outliers.

### Comparison assignment
The comparison between test condition of interest versus within-study control (e.g. asthma vs. non-asthma samples, or glucocorticoid treatment vs. baseline) is manually assigned for DE analysis.

### DE analysis
DE analysis is performed in a single comparison condition including:
* Robust multi-array average (RMA) of raw intensity signals
* DE analysis by fitting a linear model and empirical Bayes smoothing
* Batch effect adjustment

Official gene symbols are annotated to DE results. Plots are automatically generated for result visualization.

## Description of files in repository
`template_QC_report.Rmd`: R markdown codes for GSE4917 QC analysis
`template_QC_report.html`: HTML report for GSE4917 QC analysis
`template_DE_analysis_report.Rmd`: R markdown codes for GSE4917 DE analysis
`template_DE_analysis_report.html`: HTML report for GSE4917 DE analysis
`microarray folder` contains the RMD files and HTML reports for other microarray datasets used for our integrative analysis of transcriptomic data asthma and glucocorticoid response

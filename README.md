# Metabopipeline - Metabolomics data bioinformatics pipeline and data science notebooks

This pipeline aims to analyse metabolomics data, from the raw files to statistical analysis.

The pipeline is divided in three parts :
- **file conversion** : using <code>msconvert</code> from Proteowizard tools, we can convert files from vendor format (<code>.d</code>) to open source format (<code>.mzML</code>).
- **preprocessing** : using [metaboigniter](https://github.com/nf-core/metaboigniter) pipeline, we can preprocess the <code>.mzML</code> files to get the intensity peak table, identification, ...
- **visualisation and statistical analysis** : ensemble of notebooks to apply a "data science" approach to the metabolomics data outputs from the MetaboPipeline_bioinfo pipeline or from the vendor softwares (e.g., Agilent MassHunter). These notebooks allow a number of statistical and machine learning methods to be applied to analyze the metabolomics datasets, including metadata from the EPIC cohort studies


## 1 - Convert <code>.d</code> to <code>.mzML</code> files with dockerized msconvert

This part allows to easily convert files from Agilent vendor format *.d* to open-source format *.mzML*.

Corresponding [README](https://github.com/maxvincent24/metabopipeline/tree/main/msconvert).


## 2 - Run metaboigniter pipeline

This part allows to preprocess <code>.mzML</code> files with **metaboigniter** pipeline.

**For now, _metaboigniter_ pipeline is still in development.**


## 3 - Jupyter notebooks to identify potential biomarkers

This part allows to launch a JupyterLab session, with existing notebooks to analyse peak tables.

Corresponding [README](https://github.com/maxvincent24/metabopipeline/tree/main/notebooks).





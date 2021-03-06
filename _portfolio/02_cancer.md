---
title: "Lung cancer genomics"
excerpt: "<br/><img src='/images/somatic.png'>"
collection: portfolio
---

## Project Title:
* Scientific and Methodological Advancement in Liquid Biopsies to Further the Development of **Lung Cancer-Based precision Medicine**
  * Project PI: Donald Johann Jr, UAMS, Little Rock; Co-PI: Andy Pereira, U Arkansas, Fayetteville
  * [weblink](https://journals.sagepub.com/doi/abs/10.1177/1535370217750087)  


## Description
Whole exome and whole genome sequence data analysis workflow development for identification of somatic SNVs and InDels in tumor samples. Data from the study "Genomic Sequencing of Lung Adenocarcinoma (dbGAPaccession phs000488)" was downloaded for pipeline development. This dataset contains matched Tumor Normal (TN) paired-end sequencing samples from 30 patients, 8 of which also have their corresponding genome sequencing samples available. We used this dataset for sensitivity analysis of various variant calling software. The [Muffin](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-016-0989-x) algorithm was then used to fuse mutation information with human lung gene interaction network from [the GIANT server](http://giant.princeton.edu/download/) to reprioritize passenger somatic mutations likely involved in lung cancer. 
The workflow is available as a [docker container](https://hub.docker.com/r/pereiralab/wes){: .btn .btn-outline}.  

	
 



---
title: "Lung cancer genomics"
excerpt: "<br/><img src='/images/somatic.png'>"
collection: portfolio
---

Analysis workflow development for identification of somatic SNVs and InDels from tumor WGS and WES samples. NGS data from the study Genomic Sequencing of Lung Adenocarcinoma (dbGAPaccession phs000488) was downloaded for analysis pipeline development. This dataset contains matched Tumor Normal (TN) Whole Exome paired-end Sequencing (WES) samples from 30patients, 8 of which also have their corresponding Whole Genome Sequencing (WGS) samples available. We used this dataset for sensitivity analysis of different variant calling software. The [Muffin](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-016-0989-x) algorithm was then used to fuse mutation information with network data from [GIANT](http://giant.princeton.edu/download/) to reprioritize passenger somatic mutations likely involved in lung cancer. 
The pipeline is available as a [docker container](https://hub.docker.com/r/pereiralab/wes).  

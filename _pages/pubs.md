---
layout: archive
title: ""
permalink: /pubs/
author_profile: true
redirect_from:
  - /papers
---




This tutorial will help wet-lab biologists get started with analysis of their first RNA-seq dataset. 
You can essentially perform all these steps on platforms with user-friendly interface, 
such as the Galaxy server. But doing it on the terminal is a lot more fun, and of course saves a lot of time. 
Also, this workflow deals with analyzing RNA-seq data when a reference genome is available. 
In case if you have no reference genome available, you might want to take a shot at de novo assembly of transcriptomes, 
which is a different ballgame and hence different combination of software at play. 
I will write a separate tutorial on that sometime later.  



I am assuming that you already have access to all software listed below. 
If not, install them first using instructions given on their individual pages. 

## Prerequisites 
  
We will need the following software for the workflow 
1. [Fastqc](https://www.bioinformatics.babraham.ac.uk/projects/download.html)
2. [STAR](https://github.com/alexdobin/STAR)  
3. [Samtools](http://www.htslib.org/download/)
4. [Htseq](https://htseq.readthedocs.io/en/release_0.8.0/install.html)
5. [Multiqc](https://github.com/ewels/MultiQC) 
6. R packages limma and edgeR 


## Setting up project directory

Open the terminal and type 
<pre>
mkdir rnaproj
cd rnaproj
mkdir raw outputs genome 
mkdir genome/star_index
mkdir outputs/bams outputs/counts
mkdir outputs/bams/tmp
</pre>

This will create a directory structure we will use throughout this tutorial. 

## Obtaining tutorial data
Skip this section if you already have data to work with.
We will develop our workflow with this Arabidopsis dataset from GEO. It has two conditions
(control and drought treatment) with two replicates each. A total of four samples.

Download this data from SRA in the raw directory
<pre>
cd raw
fastq-dump 
</pre> 


## Quality check
<pre>
fastqc *.fastq.gz
multiqc .
</pre>

Click on the *.html file. How is the data per sample? quality overall? Are the ends good? needs trimming?

## Alignment 

We will use the STAR aligner to map our reads to the reference genome.
But first, we will need to create an index for the reference genome. 

<pre>
cd ../
star index 
</pre>

This will create index files in the star_index directory. Next, we will start aligning the reads in our fastq files of our first sample to the reference genome. 

Run STAR
<pre> 
star --genomeDir genome/star_index  --runThreadN 32 --readFilesIn raw/pe1 raw/pe2 --outFileNamePrefix outputs/bams/s1.bam --outSAMtype BAM Unsorted
star --genomeDir genome/star_index  --runThreadN 32 --readFilesIn raw/pe1 raw/pe2 --outFileNamePrefix outputs/bams/s1.bam --outSAMtype BAM Unsorted
star --genomeDir genome/star_index  --runThreadN 32 --readFilesIn raw/pe1 raw/pe2 --outFileNamePrefix outputs/bams/s1.bam --outSAMtype BAM Unsorted
star --genomeDir genome/star_index  --runThreadN 32 --readFilesIn raw/pe1 raw/pe2 --outFileNamePrefix outputs/bams/s1.bam --outSAMtype BAM Unsorted
</pre>

Sort with samtools
<pre>
samtools sort -@ 32 -T outputs/bams/tmp -O BAM -o outputs/bams/sorted.bam outputs/bams/s1.bam 
samtools sort -@ 32 -T outputs/bams/tmp -O BAM -o outputs/bams/sorted.bam outputs/bams/s1.bam 
samtools sort -@ 32 -T outputs/bams/tmp -O BAM -o outputs/bams/sorted.bam outputs/bams/s1.bam 
samtools sort -@ 32 -T outputs/bams/tmp -O BAM -o outputs/bams/sorted.bam outputs/bams/s1.bam 
</pre>


These four bam file contains information about where each sequenced read aligned in the reference genome. 
The bam files also contain other information such as the read quality and alignment rate. 
We can actually check what percentage of reads in each of our fastq files aligned correctly.

<pre>
cd outputs/bams/
multiqc *.bams
</pre>  

This will produce an html file looking something like this. What percentage of reads aligned in each sample? 

## Counting reads 
Our intention is to estimate expression levels of known gene models, therefore 
we will use the GTF file of Arabidopsis to count reads per gene. 
<pre>
htseq-count -r pos -f bam sorted.bam genome/gtf > outputs/counts/s1.counts
htseq-count -r pos -f bam sorted.bam genome/gtf > outputs/counts/s1.counts
htseq-count -r pos -f bam sorted.bam genome/gtf > outputs/counts/s1.counts
htseq-count -r pos -f bam sorted.bam genome/gtf > outputs/counts/s1.counts
</pre> 

You should have a total of 4 counts files for the four samples. Let's check that

<pre>
ls outputs/counts/*.counts | wc -l
</pre>

Merge the four count files using this R script. 

## Expression 
Now that we have our count files for the four samples, we will need to first normalize 
these counts before we go about estimating expression levels. 
[Why is normalization necessary?](https://hbctraining.github.io/DGE_workshop/lessons/02_DGE_count_normalization.html){:target="_blank"}

I have written an R script to normalize gene count data using 
[voom](https://genomebiology.biomedcentral.com/articles/10.1186/gb-2014-15-2-r29) 
and DE analysis using [limma](https://academic.oup.com/nar/article/43/7/e47/2414268). 
This script will also output Transcript Per Million (TPM) units as a measure of gene expression
in case if you want to compare genes within the same sample. 

<pre>
mkdir codes
wget Rscript
mv rscript codes
Rscript codes/rscript counts/countmatrix.txt genome/GTF  
</pre>






---
layout: archive
title: ""
permalink: /pubs/
author_profile: true
redirect_from:
  - /papers
---




This tutorial will help those getting started with analysis of their first RNA-seq dataset. You can essentially perform all these steps on platforms with user-friendly interface, such as the Galaxy server. But doing it on the terminal is a lot more fun, and of course saves a lot of time. 

I will not go through installing all the software we need to execute these steps. If you are working on your university’s cluster, you should already have these software installed (or you can ask the caretakers of the cluster to install it for you).  
 
Also, this workflow deals with analyzing RNA-seq data when a reference genome is available. In case if you have no reference genome available, you might want to take a shot at de novo assembly of transcriptomes, which is a different ballgame and hence different combination of software at play. I will write a separate tutorial on that sometime later.    

## Prerequisites 
  
We will need the following software for the workflow 
1. Tophat2
2. STAR 
3. multiqc
4. Htseq
5. Samtools 
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
We will develop our workflow with this Arabidopsis dataset from GEO. Run this command from the directory you want to store raw data.
<pre>cd raw
fastq-dump 
cd ..</pre> 


## Alignment

We will use the STAR aligner to map our reads to the reference genome. But first, we will need to create an index for the reference genome. 

<pre> star index </pre>

This will create index files in the star_index directory. Next, we will start aligning the reads in our fastq files of our first sample to the reference genome. 

<pre> 
star --genomeDir genome/star_index  --runThreadN 32 --readFilesIn raw/pe1 raw/pe2 --outFileNamePrefix outputs/bams/s1.bam --outSAMtype BAM Unsorted 
samtools sort -@ 32 -T outputs/bams/tmp -O BAM -o outputs/bams/sorted.bam outputs/bams/s1.bam
htseq-count -r pos -f bam sorted.bam genome/gtf > outputs/counts/s1.counts
</pre> 

Instead of running these command four times for four samples, we will simply automate these steps in a bash script  This will produce a file with .bam extension in the outputs/bams directory and count file in the outputs/count directory. To get these files for remaining three 
samples, run these four commands,and don't forget to change output file names. These bam file contains information about where each sequenced read aligned in the reference genome. 
The bam files also contain other information such as the read quality and alignment rate. We can actually check what percentage of reads in each of our fastq files aligned correctly.

<pre>
cd outputs/bams/
multiqc
</pre>  

This will produce an html file looking something like this. It shows that our alognment rate is approx.....

## Read counting






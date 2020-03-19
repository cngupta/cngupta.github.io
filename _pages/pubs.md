---
layout: archive
title: ""
permalink: /pubs/
author_profile: true
redirect_from:
  - /papers
---




This tutorial will guide you through analysis of your first RNA-seq dataset. We will go through installing software we will need. If you are working on your university’s cluster, you should already have these software installed (or you can ask the caretakers of the cluster to install it for you). In that case, skip the installation section and start working from step 2. 
 
Also, this workflow deals with analyzing RNA-seq data when a reference genome is available. In case if you have no reference genome available, you might want to take a shot at de novo assembly of transcriptomes, which is a different ballgame and hence different combination of software at play. I will write a separate tutorial on that sometime later.    

So let’s begin with getting our compute environment, aka the set of software that will work in tandem to get you through your dataset.


## Prerequisites 
  
We will need the following software for the workflow 
1. Tophat2
2. STAR 
3. multiqc
4. Htseq
5. Samtools 
6. R packages limma and edgeR 


## Setting up project directory

<pre>mkdir rnaproj</pre>
<pre>cd rnaproj</pre>
<pre>mkdir raw outputs</pre>
<pre>mkdir outputs/bams outputs/counts</pre>

## Obtaining tutorial data

We will develop our workflow with this Arabidopsis dataset from GEO. Run this command from the directory you want to store raw data.
<pre>cd raw</pre>
<pre> fastq-dump SRR3498212 SRR3498213, SRR3498215,and SRR3498216 </pre>
<pre>cd ..</pre>


## Alignment

We will use the STAR aligner to map our reads to the reference genome. But first, we will need to create an index for the reference genome. 

<pre> /path/to/star index </pre>

This will create index files in the star_index directory. Next, we will start aligning the reads in our fastq files to the reference genome. 

<pre> /path/to/star/ </pre> 

This will produce files with .bam extension in the bamfiles directory. Each of these bam file contains information about where each sequenced read aligned in the reference genome. The bam files also contain other information such as the read quality and alignment rate. We can actually check what percentage of reads in each of our fastq files aligned correctly.

<pre>multiqc</pre>  

This will produce an html file looking something like this. It shows that our alognment rate is approx.....

## Read counting
<>


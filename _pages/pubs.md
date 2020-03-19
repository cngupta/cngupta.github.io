
This tutorial will guide you through analysis of your first RNA-seq dataset. We will go through installing software we will need. If you are working on your university’s cluster, you should already have these software installed (or you can ask the caretakers of the cluster to install it for you). In that case, skip the installation section and start working from step 2. 
 
Also, this workflow deals with analyzing RNA-seq data when a reference genome is available. In case if you have no reference genome available, you might want to take a shot at de novo assembly of transcriptomes, which is a different ballgame and hence different combination of software at play. I will write a separate tutorial on that sometime later.    

So let’s begin with getting our compute environment, aka the set of software that will work in tandem to get you through your dataset.

We will develop our workflow with this Arabidopsis dataset from GEO. But our intention will be to end up with a single bash script that can be reused with any other dataset in future.

  
1. ## Setting up a project workspace
* We will need sequencing read aligners (Tophat2 and STAR), read counter (htseq) and R packages for differential expression estimations (limma and edgeR). 

* For this tutorial, I chose this Arabidopsis thaliana dataset that we can obtain from GEO. Before we begin our analysis, let’s set up a project directory under which we will create subdirectories storing results from every step of our analysis. We will also log our exact commands in a separate file. I call these files runlog. I will not explain why it is important to record what you do. 



2. ## Alignment

* We will use the STAR aligner to map our reads to the reference genome. But first, we will need to create an index for the reference genome. 

<pre> /path/to/star index </pre>

* This will create index files in the star_index directory. Next, we will start aligning the reads in our fastq files to the reference genome. 

<pre> /path/to/star/ </pre> 

 





3. Read counting and normalization 

4. Estimation of differential expression 


 



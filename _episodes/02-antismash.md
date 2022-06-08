---
title: "Secondary metabolite biosynthesis gene cluster identification"
teaching: 20
exercises: 30
questions:
- "What is antiSMASH?"
- "Which kind of analysis antiSMASH can perform?"
- "Which files extension accepts antiSMASH?"
- "How can I perform an antiSMASH analysis?"
objectives:
- "Understand antiSMASH applications."
- "Perform a Minimal antiSMASH run analysis."
- "Explore several *Streptococcus* genomes by identifying the BGCs presece and the types of secondary metabolites produced."
keypoints:
- "First key point. Brief Answer to questions. (antismash, genome mining, secondary metabolism, bacteria, bioactive coumpounds)"
---

# Secondary metabolite biosynthesis gene cluster identification

## Introduction

Within microbial genomes we can find some specific regions that take part of the biosynthesis of secondary metabolites, these sections are know as biosynthetic gene clusters, which are relevant due to the possible applications that they may have, for example: antimicrobials, antitumor, cholesterol-lowering, immunosuppressant, antiprotozoal, antihelminth, antiviral and anti-ageing activities.

antiSMASH is a pipline based on [profile hidden Markov models](https://www.ebi.ac.uk/training/online/courses/pfam-creating-protein-families/what-are-profile-hidden-markov-models-hmms/#:~:text=Profile%20HMMs%20are%20probabilistic%20models,the%20alignment%2C%20see%20Figure%202) that allow us to identify the gene clusters contained within genome sequences that encode secondary metabolites of all known broad chemical classes.

## antiSMASH input files

  antiSMASH pipeline can work with three different file formats ´GenBank´, ´FASTA´ and ´EMBL´. Both ´GeneBank´ and ´EMBL´ formats include genome annotations, while a ´FASTA´ file just comprises the nucleotides of each genome contig. 


## How to run antiSMASH 

The commandline usage of antismash is detailed in the following [repositories:](https://docs.antismash.secondarymetabolites.org/command_line/)

In summary, you will need to use your genome as the input. Then, antiSMASH will create an output folder for each of your genomes. Within this folder, you will find a single ´.gbk´ file for each of the detected Biosynthetic Gene Clusters (we will use these files for subsequent analyses) and a ´.html´ file, among others files. By openning the ´.html´ file you can explore the antiSMASH annotations.

You can run antiSMASH in two main ways **Minimal and Full-features run**, as follows:
### Minimal run
~~~
$ antismash genome.gbk
~~~
{: .language-bash}

### Full-featured run
~~~
$ antismash --cb-general --cb-knownclusters --cb-subclusters --asf --pfam2go --smcog-trees genome.gbk
~~~
{: .language-bash}

> ## Exercise 1: 
> If we run an Streptococcus agalactiae annotated sequence using antiSMASH, what results are we expected to get?
> 
> a. The substance that cluster produces
> 
> b. A prediction of the metabolite that cluster can produce
> 
> c. A prediction of the genes cluster that produces a metabolite 
>  
> > ## Solution
> > c. A prediction of the genes cluster that produces a metabolite 
> {: .solution}
{: .challenge}

## Run your own antiSMASH analysis :smiley:

First, activate GenomeMining conda environment:
~~~
$ conda activate GenomeMining
~~~
{: .language-code}

Second, run the antiSMASH command shown earlier in this lesson on the data ´.gbk´ or ´.fasta´ files. The command can be executed on one single files, all the files contained within a folder and on specific list of files, we showed you how you can perform these different cases:

### Case I - One single files
Let's choose the ´Streptococcus_agalactiae_18RS21.gbk´ file
~~~
$ antismash Streptococcus_agalactiae_18RS21.gbk
~~~
{: .language-code}

### Case II - Specific files
Let's imagine you want to run antismash only on following three specific files ´Streptococcus_agalactiae_18RS21.gbk´, ´Streptococcus_agalactiae_515.gbk´ and ´Streptococcus_agalactiae_A909.gbk´, so you could make use of ´for´ tool. As the following example.

for gbk_file in Streptococcus_agalactiae_18RS21.gbk Streptococcus_agalactiae_515.gbk Streptococcus_agalactiae_A909.gbk
do
    antismash $gbk_file
done

## Case III - All files in a folder

for gbk_file in *.gbk
do
    antismash $gbk_file
done


## Webpage
antiSMASH can be also used through this [web:](https://antismash.secondarymetabolites.org/#!/start)
You will be asked to give your email. Then, the results will be sent to you and you will be allowed to donwload a folder with the annotations.

## Understanding the output

The visualization of the results includes many diverse options. To understand all the possibilities, we suggest to read the following [tutorial:](https://docs.antismash.secondarymetabolites.org/understanding_output/)

Briefly, on the "overview" page ´.HTML´ you can find all the regions found within every analyzed record/contig (antiSMASH inputs), and summarized all these information in five main features:

* **Region:** The region number.
* **Type:** Type of the product detected by antiSMASH.
* **From,To:** The location of the region (nucleotides).
* **Most similar known cluster:** The closest compund from th MIBiG database.
* **Similarity:** Percentage of genes within the closest known compound that have significant BLAS hit (The last two columns containing comparisons to the MiBIG database will only be shown if antiSMASH was run with the KnownClusterBlast option ´--cc-mibig´).

> ## Exercise 2: Regions
> How can you calculate the size of a region?
> 
> > ## Solution
> > By calculating the difference between the initial position and the final position of the region.
> {: .solution}
{: .challenge}

{% include links.md %}

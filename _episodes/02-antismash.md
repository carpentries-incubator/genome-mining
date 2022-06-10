---
title: "Secondary metabolite biosynthetic gene cluster identification"
teaching: 20
exercises: 10
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
## Introduction

Within microbial genomes we can find some specific regions that take part of the biosynthesis of secondary metabolites, these sections are know as biosynthetic gene clusters, which are relevant due to the possible applications that they may have, for example: antimicrobials, antitumor, cholesterol-lowering, immunosuppressant, antiprotozoal, antihelminth, antiviral and anti-ageing activities.

antiSMASH is a pipline based on [profile hidden Markov models](https://www.ebi.ac.uk/training/online/courses/pfam-creating-protein-families/what-are-profile-hidden-markov-models-hmms/#:~:text=Profile%20HMMs%20are%20probabilistic%20models,the%20alignment%2C%20see%20Figure%202) that allow us to identify the gene clusters contained within genome sequences that encode secondary metabolites of all known broad chemical classes.

## antiSMASH input files

  antiSMASH pipeline can work with three different file formats `GenBank`, `FASTA` and `EMBL`. Both `GeneBank` and `EMBL` formats include genome annotations, while a `FASTA` file just comprises the nucleotides of each genome contig. 


## How to run antiSMASH 

The commandline usage of antismash is detailed in the following [repositories:](https://docs.antismash.secondarymetabolites.org/command_line/)

In summary, you will need to use your genome as the input. Then, antiSMASH will create an output folder for each of your genomes. Within this folder, you will find a single `.gbk` file for each of the detected Biosynthetic Gene Clusters (we will use these files for subsequent analyses) and a `.html` file, among others files. By openning the `.html` file you can explore the antiSMASH annotations.

You can run antiSMASH in two main ways **Minimal and Full-features run**, as follows:
### Minimal run
~~~
$ antismash genome.gbk
~~~
{: .source}

### Full-featured run
~~~
$ antismash --cb-general --cb-knownclusters --cb-subclusters --asf --pfam2go --smcog-trees genome.gbk
~~~
{: .source}

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

## Run your own antiSMASH analysis 
:smiley:

First, activate GenomeMining conda environment:
~~~
$ conda activate GenomeMining_Global
~~~
{: .source}

Second, run the antiSMASH command shown earlier in this lesson on the data `.gbk` or `.fasta` files. The command can be executed on one single files, all the files contained within a folder and on specific list of files, we showed you how you can perform these different cases:

#### **Case I** - One single files
Let's choose the ´Streptococcus_agalactiae_18RS21.gbk´ file
~~~
$ mkdir -p ~/gm_workshop/results/antismash
$ cd ~/gm_workshop/results/antismash
$ antismash --genefinding-tool=none ~/gm_workshop/results/annotated/agalactiae_A909_prokka.gbk 
~~~
{: .source}

To see the antiSMASH generated outcomes do:
~~~
$ cd  ~/gm_workshop/results/annotated/antismash/agalactiae_A909_prokka
$ tree -L 1
~~~
{: .source}

~~~
.
├── CP000114.1.region001.gbk
├── CP000114.1.region002.gbk
├── css
├── images
├── index.html
├── js
├── regions.js
├── Streptococcus_agalactiae_A909.gbk
├── Streptococcus_agalactiae_A909.json
├── Streptococcus_agalactiae_A909.zip
└── svg
~~~
{: .output}

#### **Case II** - Specific files
Let's imagine you want to run antismash only on following three specific files `Streptococcus_agalactiae_18RS21.gbk`, `Streptococcus_agalactiae_515.gbk` and `Streptococcus_agalactiae_A909.gbk`, so you could make use of `for` tool. As the following example.
~~~
for gbk_file in Streptococcus_agalactiae_18RS21.gbk Streptococcus_agalactiae_515.gbk Streptococcus_agalactiae_A909.gbk
do
    antismash $gbk_file
done
~~~
{: .language-bash}

#### **Case III** - All files in a folder
~~~
for gbk_file in *.gbk
do
    antismash $gbk_file
done
~~~
{: .language-bash}

For these lesson we will use the third case code. As outcomes you should get a folder comprised mainly by the following files:
* **`.gbk` files** For each Biosynthetic Gene cluster region found.
* **`.json` file** To know the input file name, the antiSMASH used version and the regions data (id,sequence_data)
* **`index.html` file** To visualize the outcomes from the analysis.

## Visualizing your analysis outcomes

To see the results after antiSMASH run, we need to access to the `index.html` file, in order to acces to that, we will run the following command:
~~~
$ cd Streptococcus_agalactiae_A909/
$ pwd
~~~ 
{: .source}
~~~
~/Streptococcus_agalactiae_A909
~~~
{: .output}

On your local machine, open a GIT bash terminal in the **destiny** folder and execture the following command:
~~~
$ scp -r user@ip_dir:~/Streptococcus_agalactiae_A909/* /destiny_folder
~~~ 
{: .source}

And finally, you can open the `index.html` file on your **Local** web browser.

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

> ## Exercise 2
> order the structure of this command line, which wants to know how big the region is:
> 
>  `SOURCE` `ORGANISM` `LOCUS`
>  
> ~~~
>  $ grep __________ region.gbk
> ~~~
> > {: .laguage-bash}
> 
> > ## Solution
> >
> > ~~~
> > $ grep LOCUS region.gbk
> > ~~~
> > Locus contains the information of the characteristics of the sequence
> > {: .laguage-bash}
> {: .solution}
{: .challenge}

{% include links.md %}

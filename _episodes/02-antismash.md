---
title: "Secondary metabolite biosynthetic gene cluster identification"
teaching: 20
exercises: 10
questions:
- "How can I annotate knwon BGC?"
- "Which kind of analysis antiSMASH can perform?"
- "Which files extension accepts antiSMASH?"
objectives:
- "Understand antiSMASH applications."
- "Perform a Minimal antiSMASH run analysis."
- "Explore several *Streptococcus* genomes by identifying the BGCs presece and the types of secondary metabolites produced."
keypoints:
- "antiSMASH is a bioinformatic tool to identify BGC"
- "antiSMASH can be used as a web-based tool or as stand-alone command-line tool"
---
## Introduction

Within microbial genomes we can find some specific regions that 
take part of the biosynthesis of secondary metabolites, these 
sections are know as biosynthetic gene clusters, which are relevant 
due to the possible applications that they may have, for example: 
antimicrobials, antitumor, cholesterol-lowering, immunosuppressant, 
antiprotozoal, antihelminth, antiviral and anti-ageing activities.

antiSMASH is a pipline based on 
[profile hidden Markov models](https://www.ebi.ac.uk/training/online/courses/pfam-creating-protein-families/what-are-profile-hidden-markov-models-hmms/#:~:text=Profile%20HMMs%20are%20probabilistic%20models,the%20alignment%2C%20see%20Figure%202) 
that allow us to identify the gene clusters contained within genome 
sequences that encode secondary metabolites of all known broad 
chemical classes.

## antiSMASH input files

antiSMASH pipeline can work with three different file formats `GenBank`, 
`FASTA` and `EMBL`. Both `GeneBank` and `EMBL` formats include genome 
annotations, while a `FASTA` file just comprises the nucleotides of 
each genome contig. 


## Running antiSMASH 

The commandline usage of antismash is detailed in the following [repositories:](https://docs.antismash.secondarymetabolites.org/command_line/)

In summary, you will need to use your genome as the input. Then, 
antiSMASH will create an output folder for each of your genomes. 
Within this folder, you will find a single `.gbk` file for each of 
the detected Biosynthetic Gene Clusters (we will use these files 
for subsequent analyses) and a `.html` file, among others files. 
By openning the `.html` file you can explore the antiSMASH annotations.

You can run antiSMASH in two main ways **Minimal and Full-features run**, as follows:  
  
|Run type   | command                                 |  
|-----------|-----------------------------------------|  
|Minimal run| antismash genome.gbk|  
|Full-featured run |antismash --cb-general --cb-knownclusters --cb-subclusters --asf --pfam2go --smcog-trees genome.gbk|  


> ## Exercise 1: 
> If you run an _Streptococcus agalactiae_ annotated genome using antiSMASH, what results do you expect?
> 
> a. The substances that a cluster produces
> 
> b. A prediction of the metabolites that the clusters can produce
> 
> c. A prediction of genes that belongs to a biosynthetic cluster 
>  
> > ## Solution  
> > a. False. antiSMASH is not an algorithm devoted to substances prediction    
> > b. False. Although antiSMASH does have some information about metabolites
> > produced by similar clusters, this is not its main purpose.  
> > c. True. AntiSMASH compares domains and performs a prediction of the genes 
> > that belong to biosynthetic gene clusters.   
> {: .solution}
{: .challenge}

## Run your own antiSMASH analysis 

First, activate GenomeMining conda environment:
~~~
$ conda deactivate
$ conda activate GenomeMining_Global
~~~
{: .source}

Second, run the antiSMASH command shown earlier in this lesson 
on the data `.gbk` or `.fasta` files. The command can be executed 
on one single files, all the files contained within a folder and 
on specific list of files, we showed you how you can perform 
these different cases:

### Running antiSMASH in a single file
Let's choose the annotated file ´agalactiae_A909_prokka.gbk´ file
~~~
$ mkdir -p ~/gm_workshop/results/antismash  
$ cd ~/gm_workshop/results/antismash  
$ antismash --genefinding-tool=none ~/gm_workshop/results/annotated/Streptococcus_agalactie_A909.prokka.gbk    
~~~
{: .language-bash}

To see the antiSMASH generated outcomes do:
~~~
$ cd ~/gm_workshop/results/antismash/Streptococcus_agalactie_A909.prokka
$ tree -L 1
~~~
{: .language-bash}

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


### Runing antiSMASH over a list of files 
Now, imagine that you want to run antiSMASH over all
_Streptococcus agalactiae_ annotated genomes. Lets use 
a `for` cycle and `*` as a wildcard to run antiSMASH
over all files that starts with "S" in the annotated directory.    
  
~~~
$ for gbk_file in  ~/gm_workshop/results/annotated/S*.gbk
$ do
>    antismash --genefinding-tool=none $gbk_file
> done
~~~
{: .language-bash}

## Visualizing antiSMASH results   
To see the results after an antiSMASH run, we need to access to 
the `index.html` file. ¿Where is this file?   
~~~
$ cd Streptococcus_agalactie_A909.prokka
$ pwd
~~~ 
{: .language-bash}
~~~
~/gm_workshop_results/antismash/Streptococcus_agalactie_A909.prokka
~~~
{: .output}

As outcomes you should get a folder comprised mainly by the following files:
* **`.gbk` files** For each Biosynthetic Gene cluster region found.
* **`.json` file** To know the input file name, the antiSMASH used 
      version and the regions data (id,sequence_data)
* **`index.html` file** To visualize the outcomes from the analysis.


In order to acces to that results, we can use scp protocol to 
download the directory in your local computer.

On your local machine, open a GIT bash terminal in the 
**destiny** folder and execture the following command:
~~~
$ scp -r user@bioinformatica.matmor.unam.mx:~/gm_workshop_results/antismash/S*A909.prokka/* ~/Downloads/.
~~~ 
{: .language-bash}

Once in your local machine, you can open the `index.html` 
file on your local web browser.

## Understanding the output

The visualization of the results includes many diverse options. 
To understand all the possibilities, we suggest to read the following [tutorial:](https://docs.antismash.secondarymetabolites.org/understanding_output/)

Briefly, on the "overview" page ´.HTML´ you can find all the regions 
found within every analyzed record/contig (antiSMASH inputs), and 
summarized all these information in five main features:

* **Region:** The region number.
* **Type:** Type of the product detected by antiSMASH.
* **From,To:** The location of the region (nucleotides).
* **Most similar known cluster:** The closest compund from th MIBiG database.
* **Similarity:** Percentage of genes within the closest known compound that have significant BLAS hit (The last two columns containing comparisons to the MiBIG database will only be shown if antiSMASH was run with the KnownClusterBlast option ´--cc-mibig´). 

## antiSMASH web services
antiSMASH can be also used in an oline server in the 
[antiSMASH website:](https://antismash.secondarymetabolites.org/#!/start)
You will be asked to give your email. Then, the results
will be sent to you and you will be allowed to donwload a 
folder with the annotations.

#### Exercise run antiSMASH over _thermpohilus_ 

> ## Exercise 2 
> Let's imagine you want to run antismash only on the _S. thermophilus_ annotated genomes.   
>  
> ~~~
>  done  
>    antismash --genefinding-tool=none $__  
>  for ___ in  ____________  
> do  
> ~~~
> > {: .laguage-bash}
> 
> > ## Solution
> >  First we need to start the for cycle: `for mygenome in ~/gm_workshop/results/annotated/S*.gbk`  
> >  note that we are using the name `mygenome` as the variable name in the for cycle.    
> >  Then you need to use the reserved word `do`  to start the cycle.     
> >  Then you have to call antismash over your variable `mygenome`. Remember the `$` before your variable
> >  to indicate to bash that now you are using the value of the variable.   
> >  Finally, use the reserved word `done` to finish the cycle.    
> > ~~~
> >  for variable in ~/gm_workshop/results/annotated/S*.gbk  
> >    do  
> >     antismash --genefinding-tool=none $mygenome  
> >    done   
> > ~~~ {: .laguage-bash}
> >
> {: .solution}
{: .challenge}


> ## Exercise 3 The size of a region.  
> Sort the structure of the next commands that attempt to know the size of a region:
> 
>  `SOURCE` `ORGANISM` `LOCUS`  
>  `head` `grep`  
> ~~~
>  $ _____  region.gbk  
>  $ _____ __________ region.gbk  
> ~~~
> >{: .laguage-bash}
> 
> Apply your solution to get the size of the first region of _S. agalactiae_ A909
> 
> > ## Solution
> >
> > ~~~
> > $ cd ~/gm_workshop/results/antismash  
> > $ head Streptococcus_agalactie_A909.prokka/CP000114.1.region001.gbk 
> > $ grep LOCUS Streptococcus_agalactie_A909.prokka/CP000114.1.region001.gbk 
> > ~~~
> > Locus contains the information of the characteristics of the sequence
> > {: .laguage-bash}
> > ~~~
> > LOCUS       CP000114.1             42196 bp    DNA     linear   UNK 13-JUN-2022 
> > ~~~
> > In this case the size of the region is 42196 bp
> > {: .output}
> {: .solution}
{: .challenge}

{% include links.md %}

---
title: "Secondary metabolite biosynthetic gene cluster identification"
teaching: 20
exercises: 10
questions:
- "How can I annotate known BGC?"
- "Which kind of analysis antiSMASH can perform?"
- "Which file extension accepts antiSMASH?"
objectives:
- "Understand antiSMASH applications."
- "Perform a Minimal antiSMASH run analysis."
- "Explore several *Streptococcus* genomes by identifying the BGCs presence and the types of secondary metabolites produced."
keypoints:
- "antiSMASH is a bioinformatic tool capable of identifying, annotating and analysing secondary metabolite BGC"
- "antiSMASH can be used as a web-based tool or as stand-alone command-line tool"
- "The file extensions accepted by antiSMASH are GenBank, FASTA and EMBL"
---
## Introduction

Within microbial genomes we can find some specific regions that
take part of the biosynthesis of secondary metabolites, these
sections are know as Biosynthetic Gene Clusters, which are relevant
due to the possible applications that they may have, for example:
antimicrobials, antitumor, cholesterol-lowering, immunosuppressant,
antiprotozoal, antihelminth, antiviral and anti-ageing activities.

antiSMASH is a pipeline based on
[profile hidden Markov models](https://www.ebi.ac.uk/training/online/courses/pfam-creating-protein-families/what-are-profile-hidden-markov-models-hmms/#:~:text=Profile%20HMMs%20are%20probabilistic%20models,the%20alignment%2C%20see%20Figure%202)
that allow us to identify the gene clusters contained within genome
sequences that encode secondary metabolites of all known broad
chemical classes.

## antiSMASH input files

antiSMASH pipeline can work with three different file formats `GenBank`,
`FASTA` and `EMBL`. Both `GenBank` and `EMBL` formats include genome
annotations, while a `FASTA` file just comprises the nucleotides of
each genomic contig.


## Running antiSMASH

The command line usage of antiSMASH is detailed in the following [repositories:](https://docs.antismash.secondarymetabolites.org/command_line/)

In summary, you will need to use your genome as the input. Then,
antiSMASH will create an output folder for each of your genomes.
Within this folder, you will find a single `.gbk` file for each of
the detected Biosynthetic Gene Clusters (we will use these files
for subsequent analyses) and a `.html` file, among other files.
By opening the `.html` file you can explore the antiSMASH annotations.

You can run antiSMASH in two ways **Minimal and Full-featured run**, as follows:  
 
|Run type   | Command                             	|  
|-----------|-----------------------------------------|  
|Minimal run| antismash genome.gbk|  
|Full-featured run |antismash --cb-general --cb-knownclusters --cb-subclusters --asf --pfam2go --smcog-trees genome.gbk|  


> ## Exercise 1: antiSMASH scope
> If you run an _Streptococcus agalactiae_ annotated genome using antiSMASH, what results do you expect?
>
> a. The substances that a cluster produces
>
> b. A prediction of the metabolites that the clusters can produce
>
> c. A prediction of genes that belong to a biosynthetic cluster
>  
> > ## Solution  
> > a. False. antiSMASH is not an algorithm devoted to substance prediction.    
> > b. False. Although antiSMASH does have some information about metabolites
> > produced by similar clusters, this is not its main purpose.  
> > c. True. antiSMASH compares domains and performs a prediction of the genes
> > that belong to biosynthetic gene clusters.   
> {: .solution}
{: .challenge}

## Run your own antiSMASH analysis

First, activate GenomeMining conda environment:
~~~
$ conda deactivate
$ conda activate /miniconda3/envs/GenomeMining_Global
~~~
{: .language-bash}

Second, run the antiSMASH command shown earlier in this lesson
on the data `.gbk` or `.fasta` files. The command can be executed
either in one single file, all the files contained within a folder or
in a specific list of files. Here we show how it can be performed in
these three different cases:

### Running antiSMASH in a single file
Choose the annotated file ´agalactiae_A909_prokka.gbk´
~~~
$ mkdir -p ~/pan_workshop/results/antismash  
$ cd ~/pan_workshop/results/antismash  
$ antismash --genefinding-tool=none ~/pan_workshop/results/annotated/Streptococcus_agalactiae_A909.prokka.gbk    
~~~
{: .language-bash}

In order to see the antiSMASH generated outcomes do:
~~~
$ tree -L 1 ~/pan_workshop/results/antismash/Streptococcus_agalactiae_A909.prokka
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


### Running antiSMASH over a list of files
Now, imagine that you want to run antiSMASH over all
_Streptococcus agalactiae_ annotated genomes. Use
a `for` cycle and `*` as a wildcard to run antiSMASH
over all files that start with "S" in the annotated directory.    
 
~~~
$ for gbk_file in ~/pan_workshop/results/annotated/S*.gbk
> do
>	antismash --genefinding-tool=none $gbk_file
> done
~~~
{: .language-bash}

## Visualizing antiSMASH results   
In order to see the results after an antiSMASH run, we need to access to
the `index.html` file. Where is this file located?   
~~~
$ cd Streptococcus_agalactiae_A909.prokka
$ pwd
~~~
{: .language-bash}
~~~
~/pan_workshop/results/antismash/Streptococcus_agalactiae_A909.prokka
~~~
{: .output}

As outcomes you should get a folder comprised mainly by the following files:
* **`.gbk` files** For each Biosynthetic Gene cluster region found.
* **`.json` file** To know the input file name, the antiSMASH used
  	version and the regions data (id,sequence_data).
* **`index.html` file** To visualize the outcomes from the analysis.


In order to access these results, we can use scp protocol to
download the directory in your local computer.

If using `scp` , on your local machine, open a GIT bash terminal in the
**destiny** folder and execute the following command:
~~~
$ scp -r user@bioinformatica.matmor.unam.mx:~/pan_workshop/results/antismash/S*A909.prokka/* ~/Downloads/.
~~~
{: .language-bash}

If using R-studio then in the left panel, chose the "more" option,
and "export" your file to your local computer. Decompress the
 Streptococcus_agalactiae_A909.prokka.zip file.  

Once in your local machine, in the directory Streptococcus_agalactiae_A909.prokka
open the `index.html` file on your local web browser.

## Understanding the output
The visualization of the results includes many different options.
To understand all the possibilities, we suggest to read the following [tutorial:](https://docs.antismash.secondarymetabolites.org/understanding_output/)

Briefly, in the "overview" page ´.HTML´ you can find all the regions
found within every analyzed record/contig (antiSMASH inputs), and
summarized all these information in five main features:

* **Region:** The region number.
* **Type:** Type of the product detected by antiSMASH.
* **From,To:** The location of the region (nucleotides).
* **Most similar known cluster:** The closest compound from th MIBiG database.
* **Similarity:** Percentage of genes within the closest known
compound that have significant BLAST hit (The last two columns
containing comparisons to the MIBiG database will only be shown
if antiSMASH was run with the KnownClusterBlast option ´--cc-mibig´).

## antiSMASH web services
antiSMASH can also be used in an online server in the
[antiSMASH website:](https://antismash.secondarymetabolites.org/#!/start)
You will be asked to give your email. Then, the results
will be sent to you and you will be allowed to donwload a
folder with the annotations.

#### Exercises and discussion

> ## Exercise 2: NCBI and antiSMASH webserver  
> Run antiSMASH web server over _S. agalactiae_ A909. First explore the
> NCBI assembly database to obtain the accession. Get the id of your results.   
>
> > ## Solution
> > 1. Go to [NCBI](https://www.ncbi.nlm.nih.gov/) and search _S. agalactiae_ A909.  
> > 2. Choose assembly database and copy the GenBank sequence Id in the bottom of the site.    
> > 3. Go to [antiSMASH](https://antismash.secondarymetabolites.org/#!/start)    
> > 4. Choose the accession from NCBI and paste `CP000114.1`    
> > 5. Run antiSMASH and paste in the collaborative document your results id
> >  example ` bacteria-cbd13a47-8095-495f-957c-dcf58c261529`  
> > {: .output}
> {: .solution}
{: .challenge}


> ## Exercise 3: Run antiSMASH over _thermophilus_
> With the following information, generate the script to run antiSMASH only on the _S. thermophilus_ annotated genomes.   
>  
> ~~~
>  done  
>	antismash --genefinding-tool=none $__  
>  for ___ in  ____________  
> do  
> ~~~
> > {: .language-bash}
>
> > ## Solution
> >  1. First, we need to start the for cycle: `for mygenome in ~/pan_workshop/results/annotated/S*.gbk`  
> >  note that we are using the name `mygenome` as the variable name in the for cycle.
> >   	 
> >  2. Then you need to use the reserved word `do`  to start the cycle.	 
> >    
> >  3. Then you have to call antiSMASH over your variable `mygenome`. Remember the `$` before your variable
> >  to indicate to bash that now you are using the value of the variable.
> > 	 
> >  4. Finally, use the reserved word `done` to finish the cycle.    
> > ~~~
> >  for variable in ~/pan_workshop/results/annotated/t*.gbk  
> >	do  
> > 	antismash --genefinding-tool=none $mygenome  
> >	done   
> > ~~~ {: .language-bash}
> >
> {: .solution}
{: .challenge}


> ## Exercise 4: The size of a region  
> Sort the structure of the next commands that attempt to know the size of a region:
>
>  `SOURCE` `ORGANISM` `LOCUS`  
>  `head` `grep`  
> ~~~
>  $ _____  region.gbk  
>  $ _____ __________ region.gbk  
> ~~~
> {: .language-bash}
>
> Apply your solution to get the size of the first region of _S. agalactiae_ A909
>
> > ## Solution
> >
> > ~~~
> > $ cd ~/pan_workshop/results/antismash  
> > $ head Streptococcus_agalactiae_A909.prokka/CP000114.1.region001.gbk
> > $ grep LOCUS Streptococcus_agalactiae_A909.prokka/CP000114.1.region001.gbk
> > ~~~
> > Locus contains the information of the characteristics of the sequence
> > {: .language-bash}
> > ~~~
> > LOCUS   	CP000114.1         	42196 bp	DNA 	linear   UNK 13-JUN-2022
> > ~~~
> > {: .language-bash}
> > In this case the size of the region is 42196 bp
> > {: .output}
> {: .solution}
{: .challenge}


> ## Discussion 1: BGC classes in _Streptococcus_
>
> What BGC classes does the genus _Streptococcus_ have ?   
>
> > ## Solution
> >
> > In antiSMASH website output of A909 strain we see clusters of two classes, T3PKS and arylpolyene. Nevertheless, this is only one _Streptococcus_ in order to infer all BGC classes in the genus we need to run antiSMASH in more genomes.
> {: .solution}
{: .discussion}

{% include links.md %}




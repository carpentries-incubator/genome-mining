---
title: "Antismash"
teaching: 20
exercises: 30
questions:
- "What is antiSMASH?"
- "Which kind of analysis antiSMASH can perform?"
- "Which files extension accepts antiSMASH?"
objectives:
- "Understand antiSMASH applications."
- "Perform a Minimal antiSMASH run analysis."
- "Explore several Streptococcus genomes by identifying their BGCs and types of their produced secondary metabolites."
keypoints:
- "First key point. Brief Answer to questions. (antismash, genome mining, secondary metabolism, bacteria, bioactive coumpounds)"
---

# antiSMASH

## Introduction

Within microbial genoms we can find some specific regions that take part of the biosynthesis of secondary metabolites, these sections are know as biosynthetic gene clusters, which are relevant due to the possible applications that they may have, for example: antimicrobials, antitumor, cholesterol-lowering, immunosuppressant, antiprotozoal, antihelminth, antiviral and anti-ageing activities.

antiSMASH is a pipline based on [profile hidden Markov models](https://en.wikipedia.org/wiki/Hidden_Markov_model#:~:text=A%20hidden%20Markov%20model%20(HMM,of%20in%20a%20known%20way.) that allow us to identify the gene clusters contained within genome sequences that encode secondary metabolites of all known broad chemical classes.

# antiSMASH input files

  antiSMASH pipeline can work with three different file formats ´GenBank´, ´FASTA´ and ´EMBL´. Both ´GeneBank´ and ´EMBL´ formats include genome annotations, while a ´FASTA´ file just comprises the nucleotides of each genome contig. 


# run antiSMASH 

The commandline usage of antismash is detailed in the following [repositories:](https://docs.antismash.secondarymetabolites.org/command_line/)

In summary, you will need to use your genome as the input. Then, antiSMASH will create an output folder for each of your genomes. Within this folder, you will find a single ´.gbk´ file for each of the detected Biosynthetic Gene Clusters (we will use these files for subsequent analyses) and a ´.html´ file, among others files. By openning the ´.html´ file you can explore the antiSMASH annotations.

You can run antiSMASH in two main ways **Minimal and Full-features run**, as follows:
## Minimal run
~~~
$ antismash genome.gbk
~~~
{: .language-bash}

## Full-featured run
~~~
$ antismash --cb-general --cb-knownclusters --cb-subclusters --asf --pfam2go --smcog-trees genome.gbk
~~~
{: .language-bash}

# antiSMASH extra parameters

There are some extra analyses that can be done adn information that can be obtained.

--------
### Options
--------

| Command               | Description |
| :---                  |    :----:   |
| -h, --help            | Show this help text. |
| --help-showall        | Show full lists of arguments on this help text. |
|  -c CPUS, --cpus CPUS |  How many CPUs to use in parallel. (default: 1) |


| Analysis option | Description |
| :----: | :----: |
| --cc-mibig                    | Run a comparison against the MIBiG dataset |

## Webpage
AntiSMASH can be also used through this [web:](https://antismash.secondarymetabolites.org/#!/start)
You will be asked to give your email. Then, the results will be sent to you and you will be allowed to donwload a folder with the annotations.

# Understanding the output

The visualization of the results includes many diverse options. To understand all the possibilities, we suggest to read the following [tutorial:](https://docs.antismash.secondarymetabolites.org/understanding_output/)

Briefly, on the "overview" page ´.HTML´ you can find all the regions found within every analyzed record/contig (antiSMASH inputs), and summarized all these information in five main features:

* **Region:** The region number.
* **Type:** Type of the product detected by antiSMASH.
* **From,To:** The location of the reagion (nucleotides).
* **Most similar known cluster:** The closest compund from th MIBiG database.
* **Similarity:** Percentage of genes within the closest known compound that have significant BLAS hit (The last two columns containing comparisons to the MiBIG database will only be shown if antiSMASH was run with the KnownClusterBlast option).

## Webpage
AntiSMASH can be also used through its [web platform version:](https://antismash.secondarymetabolites.org/#!/start)
You will be asked to give your email. Then, the results will be sent to you and you will be allowed to donwload a folder with the annotations.

> ## Exercise 2. Regions `.challenge`
> How can you calculate the size of a region?
> 
> > ## Solution
> > By calculating the difference between the initial position and the final position of the region.
> {: .solution}
{: .challenge}


{% include links.md %}

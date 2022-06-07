---
title: "Antismash"
teaching: 20
exercises: 30
questions:
- "What is antiSMASH?"
- "Which kind of analysis antiSMASH can perform?"
- "Which files extension accepts antiSMASH?"
objectives:
- "Understand how antiSMASH applications."
- "Understand the importance of metadata and potential metadata standards."
- "Explore common formatting challenges in spreadsheet data."
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

## Full-featured run
~~~
$ antismash --cb-general --cb-knownclusters --cb-subclusters --asf --pfam2go --smcog-trees genome.gbk
~~~

However, there are many extra analyses that can be done. See the following sections to understand all the posibilities.

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


Output options:

  --output-dir OUTPUT_DIR
                        Directory to write results to.
  --output-basename OUTPUT_BASENAME
                        Base filename to use for output files within the output directory.
  --html-title HTML_TITLE
                        Custom title for the HTML output page (default is input filename).
  --html-description HTML_DESCRIPTION
                        Custom description to add to the output.
  --html-start-compact  Use compact view by default for overview page.


## Webpage
AntiSMASH can be also used through this web: https://antismash.secondarymetabolites.org/#!/start 
You will be asked to give your email. Then, the results will be sent to you and you will be allowed to donwload a folder with the annotations.

# Understanding the output

The visualization of the results includes many diverse options. To understand all the possibilities, we suggest to read the following tutorial: https://docs.antismash.secondarymetabolites.org/understanding_output/ 

Briefly, on the "overview" page you will find the number and type of BGCs annotated in your genome. By clicking on a specific BGC, you will find its gene structure (Figure Xa), its module composition (only for somy BGC types) (Figure Xb), and the similarity of your cluster with already described BGCs and published in the antiSMASH database (Figure Xc) or in the MiBIG database (Figure Xd). 

![Antismash](https://github.com/AxelRamosGarcia/Genome-Mining/blob/gh-pages/fig/antismash_cluster.png)
Figure X

{% include links.md %}

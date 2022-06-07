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

<div style="text-align: justify"> Within microbial genoms we can find some specific regions that take part of the biosynthesis of secondary metabolites, these sections are know as biosynthetic gene clusters, which are relevant due to the possible applications that they may have, for example: antimicrobials, antitumor, cholesterol-lowering, immunosuppressant, antiprotozoal, antihelminth, antiviral and anti-ageing activities.

 Antismash is a pipline based on [profile hidden Markov models](https://en.wikipedia.org/wiki/Hidden_Markov_model#:~:text=A%20hidden%20Markov%20model%20(HMM,of%20in%20a%20known%20way.) that allow us to identify the gene clusters contained within genome sequences that encode secondary metabolites of all known broad chemical classes. </div>

# run AntiSMASH 

The commandline usage of antismash is detailed in the following repositories: https://docs.antismash.secondarymetabolites.org/command_line/ and https://github.com/antismash/antismash

In sum, you will need to use your genome as the input (see "Arguments" section). Then, antiSMASH will create an output folder for each of your genomes. Within this folder, you will find a single .gbk file for each of the detected Biosynthetic Gene Clusters (we will use these files for subsequent analyses) and a .html file, among others files. By clicking in the .html file you can explore the antiSMASH annotations.

An example of a basic usage is:
~~~
$ antismash genome.gbk
~~~

However, there are many extra analyses that can be done. See the following sections to understand all the posibilities.

## Arguments

antiSMASH can work with three different
arguments:
  SEQUENCE  GenBank/EMBL/FASTA file(s) containing DNA.

  antiSMASH package can work with three different file formats GenBank, FASTA and EMBL. Both GeneBank nad EMBL formats include genome annotations, while a FASTA file just comprises the nucleotides of each genome contig. 

1. GenBank format consists of two main sections, annotation and a sequence. The annotation section begins at the "Locus" header and the sequence sections at the "origin" word. Finally, the end section can be recognized due to the mark "//". AntiSMASH developers recomend using RAST (https://rast.nmpdr.org/) genome annotations as input file.

2. EMBL format also includes gene annotations. Each entry starts with its identifier ("ID "), then the sequence is preceded by a line starting with "SQ", and again, the end of the sequence is recognized by two slashes ("//"). 

3. Fasta format consists of one line which starts with a ">" sign, followed by a textual description of sequence (nucleotides). Since it is not part of the official of the format, softwares can choose to ignore this, when it is present. One or more lines containing the sequences itself. In case you use your un-annotated genome in fasta file format, antiSMASH will perform a gene calling through the software selected with "--genefinding-tool".


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
| --taxon {bacteria,fungi}      | Taxonomic classification of input sequence. (default: bacteria) |
| --fullhmmer                   | Run a whole-genome HMMer analysis. |  
| --cassis                      | Motif based prediction of SM gene cluster regions. |
| --clusterhmmer                | Run a cluster-limited HMMer analysis. |
| --tigrfam                     | Annotate clusters using TIGRFam profiles. |
| --smcog-trees                 | Generate phylogenetic trees of sec. met. cluster orthologous groups. |
| --tta-threshold TTA_THRESHOLD | Lowest GC content to annotate TTA codons at (default: 0.65). |
| --cb-general                  | Compare identified clusters against a database of antiSMASH-predicted clusters. |
| --cb-subclusters              | Compare identified clusters against known subclusters responsible for synthesising precursors. |
| --cb-knownclusters            | Compare identified clusters against known gene clusters from the MIBiG database. |
| --asf                         | Run active site finder analysis. |
| --pfam2go                     | Run Pfam to Gene Ontology mapping module. |
| --rre                         | Run RREFinder precision mode on all RiPP gene clusters. |
| --cc-mibig                    | Run a comparison against the MIBiG dataset |

Gene finding options (ignored when ORFs are annotated):

  --genefinding-tool {glimmerhmm,prodigal,prodigal-m,none,error}
                        Specify algorithm used for gene finding: GlimmerHMM, Prodigal,
                        Prodigal Metagenomic/Anonymous mode, or none. The 'error' option
                        will raise an error if genefinding is attempted. The 'none' option
                        will not run genefinding. (default: error).
  --genefinding-gff3 GFF3_FILE
                        Specify GFF3 file to extract features from.

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

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

<div style="text-align: justify"> Many microbial genomes contain several biosynthetic gene clusters, which encode the biosynthesis of secondary metabolites. These molecules have shown some relevance. Their active compounds have shown: antimicrobials, antitumor, cholesterol-lowering, immunosuppressant, antiprotozoal, antihelminth, antiviral and anti-ageing activities, amongst others. The genes encoding the biosynthetic pathway responsible for the production of such a secondary metabolite are clustered together at a certain chromosome position (secondary metabolite biosynthesis gene cluster). The genetic architecture lets the possibility to detect secondary metabolite biosynthesis pathways by locating their gene clusters. Nowadays many genome sequences are available online. Based on profile hidden Markov models of genes that are specific for certain types of gene clusters, antiSMASH can accurately identify the gene clusters encoding secondary metabolites of all known broad chemical classes. antiSMASH not only detects the gene clusters, but also offers detailed sequence analysis.</div>
 
# Profile Hidden Markov Models

## Definition

Profile Hidden Markov's models are computational algorithms that predict protein structure identifying significant protein similarities letting a homologs detection. These probabilistic models:

- Encapsulate evolutionary changes that occurred in a set of related sequences.

Some applications are on gene finding, construction of genetic linkage maps (Turn multiple sequence alignment into a position-specific scoring system suitable for searching databases for remotely homologous sequences), and construction of physical maps. The most highlighted advantage is that this model has better gap dealing methods in proteins families.

![profile Markov Hidden Models](https://upload.wikimedia.org/wikipedia/commons/7/71/A_profile_HMM_modelling_a_multiple_sequence_alignment.png)

# run AntiSMASH 

The commandline usage of antismash is detailed in the following repositories: https://docs.antismash.secondarymetabolites.org/command_line/ and https://github.com/antismash/antismash

In sum, you will need to use your genome as the input (see "Arguments" section). Then, antiSMASH will create an output folder for each of your genomes. Within this folder, you will find a single .gbk file for each of the detected Biosynthetic Gene Clusters (we will use these files for subsequent analyses) and a .html file, among others files. By clicking in the .html file you can explore the antiSMASH annotations.

An example of a basic usage is:
`antismash genome.gbk`

However, there are many extra analyses that can be done. See the following sections to understand all the posibilities.

## Arguments

antiSMASH can work with three different
arguments:
  SEQUENCE  GenBank/EMBL/FASTA file(s) containing DNA.

  antiSMASH package can work with three different file formats GenBank,  FASTA and EMBL. 

1. GenBank format consists of two main sections, annotation and a sequence. The annotation section begins at the "Locus" header and the sequence sections at the "origin" word. Finally, the end section can be recognized due to the mark "//". AntiSMASH developers recomend using RAST (https://rast.nmpdr.org/) genome annotations as input file

2. Fasta format consists of one line which starts with a ">" sign, followed by a textual description of sequence. Since it is not part of the official of the format, softwares can choose to ignore this, when it is present. One or more lines containing the sequences itself. In case you use your un-annotated genome in fasta file format, antiSMASH will perform a gene calling through the software selected with "--genefinding-tool".

### FASTA format example
---
>BTBSCRYR
tgcaccaaacatgtctaaagctggaaccaaaattactttctttgaagacaaaaactttca
aggccgccactatgacagcgattgcgactgtgcagatttccacatgtacctgagccgctg
caactccatcagagtggaaggaggcacctgggctgtgtatgaaaggcccaattttgctgg
gtacatgtacatcctaccccggggcgagtatcctgagtaccagcactggatgggcctcaa
cgaccgcctcagctcctgcagggctgttcacctgtctagtggaggccagtataagcttca
gatctttgagaaaggggattttaatggtcagatgcatgagaccacggaagactgcccttc
catcatggagcagttccacatgcgggaggtccactcctgtaaggtgctggagggcgcctg
gatcttctatgagctgcccaactaccgaggcaggcagtacctgctggacaagaaggagta
ccggaagcccgtcgactggggtgcagcttccccagctgtccagtctttccgccgcattgt
ggagtgatgatacagatgcggccaaacgctggctggccttgtcatccaaataagcattat
aaataaaacaattggcatgc
---

--------
Options
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

![antismash] (https://github.com/AxelRamosGarcia/Genome-Mining/blob/gh-pages/fig/antismash_cluster.png)
Figure X

{% include links.md %}

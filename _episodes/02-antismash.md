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

"The secondary metabolism of bacteria and fungi constitutes a rich source of bioactive compounds of potential pharmaceutical value, comprising biosynthetic pathways of many chemicals that have been and are being utilized as e.g. antibiotics, cholesterol-lowering drugs or antitumor drugs. Interestingly, the genes encoding the biosynthetic pathway responsible for the production of such a secondary metabolite are very often spatially clustered together at a certain position on the chromosome; such a compendium of genes is referred to as a 'secondary metabolite biosynthesis gene cluster'. This genetic architecture has opened up the possibility for straightforward detection of secondary metabolite biosynthesis pathways by locating their gene clusters. In recent years, the costs of sequencing bacterial and fungi has dropped dramatically, and many genome sequences have become available. Based on profile hidden Markov models of genes that are specific for certain types of gene clusters, antiSMASH is able to accurately identify the gene clusters encoding secondary metabolites of all known broad chemical classes. antiSMASH not only detects the gene clusters, but also offers detailed sequence analysis."

# Profile Hidden Markov Models

## Definition

Profile Hidden Markov's models are computational algorithms that predict protein structure identifying significant protein similarities letting a homologs detection. These probabilistic models:

- Encapsulate evolutionary changes that occurred in a set of related sequences.

Some applications are on gene finding, construction of genetic linkage maps (Turn multiple sequence alignment into a position-specific scoring system suitable for searching databases for remotely homologous sequences), and construction of physical maps. The most highlighted advantage is that this model has better gap dealing methods in proteins families.

![profile Markov Hidden Models](https://upload.wikimedia.org/wikipedia/commons/7/71/A_profile_HMM_modelling_a_multiple_sequence_alignment.png)

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

arguments:
  SEQUENCE  GenBank/EMBL/FASTA file(s) containing DNA.


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

Gene finding options (ignored when ORFs are annotated):

  --genefinding-tool {glimmerhmm,prodigal,prodigal-m,none,error}
                        Specify algorithm used for gene finding: GlimmerHMM, Prodigal,
                        Prodigal Metagenomic/Anonymous mode, or none. The 'error' option
                        will raise an error if genefinding is attempted. The 'none' option
                        will not run genefinding. (default: error).
  --genefinding-gff3 GFF3_FILE
                        Specify GFF3 file to extract features from.


{% include links.md %}
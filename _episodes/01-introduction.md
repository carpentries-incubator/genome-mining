---
title: "Introduction to Genome Mining"
teaching: 10
exercises: 0
questions:
- "What is Genome Mining?"
objectives:
- "Understand that Natural products are encoded in Biosynthetic Gene Clusters."
- "Understand that Biosynthetic Gene Clusters can be identified in the genomic material."
- "Discuss bioinformatic's good practices with your colleagues."

keypoints:
- "Natural products are encoded in Biosynthetic Gene Clusters (BGCs)"
- "Genome mining describes the exploitation of genomic information with specialized algorithms intended to discover and study BGCs"
---

## Genome mining aims to find BGCs
Natural products are encoded in [Biosynthetic Gene Clusters](https://en.wikipedia.org/wiki/Metabolic_gene_cluster
) (BGCs) in Bacteria. These BGCs are clusters of genes placed together in the same genome region. These include the genes encoding the biosynthetic enzymes and those related to the metabolite's transport or resistance against antibacterial metabolites.
[Genome mining](https://en.wikipedia.org/wiki/Genome_mining) consists in analyzing genomes with specialized algorithms
designed to find some BGCs. Chemists in the last century diligently characterized some of these clusters. We have extensive databases that contain
information about which genes belong to which BGCs and some control sets of genes that do not. The use of genome mining methodologies facilitates the prioritization of BGCs for the search of novel metabolites.
Since the era of next-generation sequencing, genomes have been explored
as a source for discovering new BGCs.

<a href="{{ page.root }}/fig/Chapter1Fig1.png">
  <img src="{{ page.root }}/fig/Introduction01.png" alt="Complete pipeline of genome mining. From a single genome, this example obtains their BGC and compares them with other BGC from related genomes" width="60%" height="60%" />
</a>
[Genome Mining Wikipedia](https://en.wikipedia.org/wiki/Genome_mining)
## Chloramphenicol is a known antibiotic produced in a BGC

For example, let's look into the BGC responsible for chloramphenicol biosynthesis. This is a BGC described for the first time in a _Streptomyces venezuelae_ genome.

<a href="{{ page.root }}/fig/episode1-fig1.PNG">
  <img src="{{ page.root }}/fig/episode1-fig1.PNG" alt="MIBiG layout of the Chloramphenicol gene cluster from _Streptomyces venezuelae_ comprising 17 genes"  />
</a>
[Explore the BGC](https://mibig.secondarymetabolites.org/repository/BGC0000893/index.html#r1c1)

> ## Exercise 1: Sort the Steps to Identify BGCs Similar to Clavulanic Acid
>
> Below is a list of steps in disarray that are part of the process of identifying BGCs similar to clavulanic acid. Your task is to logically order them to establish a coherent methodology that allows the effective identification of such BGCs.
>
> **Disordered Steps:**
>
> a. Annotate the genes within the identified BGCs to predict their function.
>
> b. Compare the identified BGCs against databases of known BGCs to find similarities to clavulanic acid.
>
> c. Extract DNA from samples of interest, such as microorganism-rich soils or specific bacterial cultures.
>
> d. Conduct phylogenetic analysis of the BGCs to explore their evolutionary relationship.
>
> e. Use bioinformatics tools to assemble DNA sequences and detect potential BGCs.
>
> f. Sequence the extracted DNA using next-generation sequencing (NGS) techniques.
>
>> ## Solution
>>
>> 1. c. Extract DNA from samples of interest, such as microorganism-rich soils or specific bacterial cultures.
>> 2. f. Sequence the extracted DNA using next-generation sequencing (NGS) techniques.
>> 3. e. Use bioinformatics tools to assemble DNA sequences and detect potential BGCs.
>> 4. a. Annotate the genes within the identified BGCs to predict their function.
>> 5. d. Conduct phylogenetic analysis of the BGCs to explore their evolutionary relationship.
>> 6. b. Compare the identified BGCs against databases of known BGCs to find similarities to clavulanic acid.
> {: .solution}
{: .challenge}

## Planning a genome mining project  
Here we will provide tips and tricks to plan and execute a genome mining project.
Firstly, choose a set of genomes from taxa. In this lesson
we will be working with _S. agalactiae_ [genomes](https://zenodo.org/record/6595388#.YtD9LsFBxUJ) (Tettelin et al., 2005). Although this genus is not know
for its potential as a Natural products producer, it is good enough
to show different approaches to genome mining. Recently, metagenomes have been
considered in genome mining studies. Here are some considerations
that might be useful as a genome miner:

- Think about a research question before starting to analyze the data.  
- Remember, raw metadata should remain intact during all genome mining processes.
It could be a good idea to change its file permissions to read-only.    
- Gather as much information as metadata of
all the genomes you work with.  
- All your intermediate steps should be considered temporal
 and may be removed without risk.   
- Save your scripts using a version manager, GitHub for example.
- Share your data in public repositories.   
- Give time to make your science repeatable and help your community.    

> ## Discussion 1: Describe your project
> Tdoihasodihfo FIXME
>
> > ## Solution  
> > a. FIX ME.     
> {: .solution}
{: .challenge}

2. Donwload Genomes, Dat     
> {: .solution}
{: .challenge}



## Starting a genome mining project
Once you have chosen your set of genomes, you need to annotate the sequences. The process of genome annotation needs two steps. First, a gene calling approach (structural annotation), which looks for CDS or RNAs within the DNA sequences. Once these features have been detected, you need to assign a function for each CDS (functional annotation). This is usually done through comparison against protein databases. There are tens of bioinformatics tools to annotate genomes, but some of the most broadly used are; RAST (Aziz et al. 2008), and Prokka (Seeman, 2014). Here, we will start the genome mining lesson with  _S. agalactiae_ genomes already annotated by Prokka. You can download this data from this [repository](https://zenodo.org/record/6595388#.YtD9LsFBxUJ). The annotated genomes are written in GeneBank format (extension ".gbk"). To learn more about the basic annotation of genomes, see the lesson named ["Pangenome Analysis in Prokaryotes: Annotating Genomic Data"](https://paumayell.github.io/pangenomics/03-annotation-with-Prokka/index.html)These files are also accessible in the... **Insert introduction related to the access to the server??**

## References
- Aziz, R. K., Bartels, D., Best, A. A., DeJongh, M., Disz, T., Edwards, R. A., ... & Zagnitko, O. (2008). The RAST Server: rapid annotations using subsystems technology. BMC genomics, 9(1), 1-15.
- Seemann, T. (2014). Prokka: rapid prokaryotic genome annotation. Bioinformatics, 30(14), 2068-2069.
- Tettelin, H., Masignani, V., Cieslewicz, M. J., Donati, C., Medini, D., Ward, N. L., ... & Fraser, C. M. (2005). Genome analysis of multiple pathogenic isolates of Streptococcus agalactiae: implications for the microbial “pan-genome”. Proceedings of the National Academy of Sciences, 102(39), 13950-13955.

{% include links.md %}





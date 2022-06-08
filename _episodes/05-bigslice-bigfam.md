---
source: md
title: "BiGSlice / BiGFAM"
teaching: --
exercises: --
questions:
- "?"
- "?"
objectives:
- "Understand why we want to run `BiGSLICE` and `BiGFAM` "
- "Learn what input do we need to run `BiGSLICE` and `BiGFAM`"
- "Run an example with our _Streptococcus_ data on both softwares"
- "Understand the obtained results"
keypoints:
- ""  
- ""
- ""
---

> ## Ejercicio `.challenge`
> As we have seen the structure of the input folder for BiGSLICE is quite difficult to get. Imagine "Sekiro" wants to copy the directory structure to use it for future BigSlice inputs.
> Consider the following directory structure:
> ~~~
>    └── input_folder/                    
>        ├── datasets.tsv           
>        ├── dataset_1/
>        |   ├── genome_1A/
>        |   |   ├── genome_1A.region001.gbk
>        |   |   └── genome_1A.region002.gbk
>        |   ├── genome_1B/
>        |   |   ├── genome_1B.region001.gbk
>        |   |   └── genome_1B.region002.gbk
>        ├── dataset_2/
>        |   ├── genome_2A/
>        |   |   ├── genome_2A.region001.gbk
>        |   |   └── genome_2A.region002.gbk
>        |   ├── genome_2B/
>        |   |   ├── genome_2B.region001.gbk
>        |   |   └── genome_2B.region002.gbk
>        └── taxonomy/
>            ├── taxonomy_dataset_1.tsv
>            └── taxonomy_dataset_2.tsv                     
> ~~~
> {: .output}
> Which would be the commands to copy the directory structure without the files (just the folders)? <br>
> a)
> ~~~
> $ cp -r input_folder input_folder_copy
> $ cd input_foder_copy
> $ rm -r
> ~~~
> {: .bash}
> b)
> ~~~
> $ mv -r input_folder input_folder_copy
> $ rm input_folder_copy/dataset_1/genome_1A/* input_folder_copy/dataset_1/genome_1B/*
> $ rm input_folder_copy/dataset_2/genome_2A/* input_folder_copy/dataset_2/genome_2B/*
> $ rm input_folder_copy/taxonomy/*
> ~~~
> {: .bash}
> c)
> ~~~
> $ cp -r input_folder input_folder_copy
> $ rm input_folder_copy/dataset_1/genome_1A/* input_folder_copy/dataset_1/genome_1B/*
> $ rm input_folder_copy/dataset_2/genome_2A/* input_folder_copy/dataset_2/genome_2B/*
> $ rm input_folder_copy/taxonomy/*
> ~~~
> {: .bash}
> d)
> ~~~
> $ cp -r input_folder input_folder_copy
> $ rm input_folder_copy/dataset_1/genome_1A/* /genome_1B/*
> $ rm input_folder_copy/dataset_2/genome_2A/* /genome_2B/*
> $ rm input_folder_copy/taxonomy/*
> ~~~
> {: .bash}
> > ## Solution
> > c)
> > ~~~
> > $ cp -r input_folder input_folder_copy
> > $ rm input_folder_copy/dataset_1/genome_1A/* input_folder_copy/dataset_1/genome_1B/*
> > $ rm input_folder_copy/dataset_2/genome_2A/* input_folder_copy/dataset_2/genome_2B/*
> > $ rm input_folder_copy/taxonomy/*
> > ~~~
> > {: .bash}
> {: .solution}
{: .challenge}

> ## Exercise 2. `.challenge`  
> If you use the head -n20 on one of your .gbk files, you will obtain an output like this
>~~~
>LOCUS       AAJO01000169.1          2501 bp    DNA     linear   UNK
>DEFINITION  Streptococcus agalactiae 18RS21
>ACCESSION   AAJO01000169.1
>KEYWORDS    .
>SOURCE      Streptococcus agalactiae 18RS21.
>  ORGANISM  Streptococcus agalactiae 18RS21
>            Bacteria; Terrabacteria group; Firmicutes; Bacilli;
>            Lactobacillales; Streptococcaceae; Streptococcus; Streptococcus
>            agalactiae.
>FEATURES             Location/Qualifiers
>     source          1..2501
>                     /mol_type="genomic DNA"
>                     /db_xref="taxon:342613"
>                     /genome_md5=""
>                     /project="nselem35_342613"
>                     /genome_id="342613.37"
>                     /organism="Streptococcus agalactiae 18RS21"
>     CDS             1..213
>                     /db_xref="SEED:fig|342613.37.peg.1973"
>                     /db_xref="GO:0003735"
>~~~
>{: .output}
> As you can see, in the gbk file we can find the taxonomic information that we need to fill the taxonomic information of each genome.
> Fill in the blank spaces to complete the command that would get the organism information from the .gbk file. 
> 
> <p style="text-align: center;"> $ grep ___________ -m1 ____________ Streptococcus_agalactiae_18RS21.gbk </p>
>  <p style="text-align: center;"> -B 3 &nbsp; &nbsp; &nbsp; -A 3 &nbsp; &nbsp; &nbsp; -a  &nbsp; &nbsp; &nbsp; 'Streptococcus' &nbsp; &nbsp; &nbsp; 'ORGANISM' &nbsp; &nbsp; &nbsp; 'gbk'</p>
> To obtain the next result:
> 
> ~~~
>  ORGANISM  Streptococcus agalactiae 18RS21
>            Bacteria; Terrabacteria group; Firmicutes; Bacilli;
>            Lactobacillales; Streptococcaceae; Streptococcus; Streptococcus
>            agalactiae.
> ~~~
> {: .output}  
> 
> > ## Solution
> > ~~~
> > $ grep 'ORGANISM' -m1 -A3 Streptococcus_agalactiae_18RS21.gbk
> > ~~~
> > {: .bash}
> {: .solution}
{: .challenge}

> ## Discussion
> Considering the results in the runs tab, we can see that there are a lot of Gene Cluster Families that have only one cluster associated to it (GCF_1, GCF_2, GCF_5, GCF_7). <br>
> What does this tell us about the metabolites diversity of the Streptococcus sample?
> 
{: .discussion}   

<!-- |-------------------+--------------------------------------------------------|
|        GCF        |                     #core members                      |
|:-----------------:+:------------------------------------------------------:|
|       GCF_1       |                            6                           |
|-------------------+--------------------------------------------------------|
|       GCF_2       |                            5                           |
|-------------------+--------------------------------------------------------|
|       GCF_3       |                            5                           |
|-------------------+--------------------------------------------------------|
|       GCF_4       |                            6                           |
|-------------------+--------------------------------------------------------| -->

> ## Discussion
>
> |-------------------+--------------------------------------------------------|
> |        GCF        |                     #core members                      |
> |:-----------------:+:------------------------------------------------------:|
> |       GCF_1       |                            6                           |
> |-------------------+--------------------------------------------------------|
> |       GCF_2       |                            5                           |
> |-------------------+--------------------------------------------------------|
> |       GCF_3       |                            5                           |
> |-------------------+--------------------------------------------------------|
> |       GCF_4       |                            6                           |
> |-------------------+--------------------------------------------------------|
>  
{: .discussion}   

{% include links.md %}

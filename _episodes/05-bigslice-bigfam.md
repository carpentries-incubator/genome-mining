---
source: md
title: "BiGSlice / BiGFAM"
teaching: --
exercises: --
questions:
- "Why to use BiGSlice / BiGFAM?"
- "How to run a BGC analysis with BiGSlice / BiGFAM?"
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

# BiGSLICE and BiGFAM a set of tools to compare the microbial metabolic diversity


## BiGSLICE 

Around the curriculum, we have been learning about the metabolic 
capability of bacteria lineages encoded in BGCs. Before we start this 
lesson, let's remember that the products of these clusters are 
biomolecules that are (mostly) not essential for life. They take 
the role of "tools" that offer some ecological and physiological 
advantage to the bacterial lineage producing it. 

<a href="../fig/02-05-01.png">
  <img src="../fig/01-05-01.png" alt="Aquí va el texto que describe a la imagen." />
</a>

The presence/abscence of a set of BGCs in a genome, can be associated 
to the ecological niches and (micro)environments which the linage faces. 

The counterpart of this can be taked as how biosynthetically diverse 
a bacterial lineage can be because of its environment.

<a href="../fig/02-05-02.png">
  <img src="../fig/01-05-02.png" alt="Aquí va el texto que describe a la imagen." />
</a>

To answer some of this questions, we need a way to compare the metabolic 
capabilities of a set of diverse bacterial lineages. One way to do this 
is to compare the state (identity) of homologous BGCs. The homologous 
clusters that share a similar domain arquitecture and in consequnece 
will produce a similar metabolite, are grouped into a bigger group that 
we call **Gene Cluster Families (GCFs)**. 

As seen in BiG-SCAPE, there are some programs capable of clustering BGCs 
in GCFs, _e.g._[ ClusterFinder](https://github.com/petercim/ClusterFinder) and [DeepBGC](https://github.com/Merck/deepbgc). `BiG-SLICE` is a 
software that has been [designed](https://academic.oup.com/gigascience/article/10/1/giaa154/6092777) to do this work in less time even 
when dealing with large datasets (1.2 million BGCs). This 
characteristic makes it a good tool to compare the metabolic 
diversity of several bacterial lineages.

### The input for BiGSLICE

First of all, let's activate the conda environment where `BiGSLICE` 
has been installed and all the needed softwares for its usage:

~~~
$ conda activate GenomeMining
~~~
{: .bash}

You will have now a `(GenomeMining)` label at the beggining of the 
promt line.

If we seek for help using the `--help` flag of `bigslice`, we can get 
a first glance at the input that we need:

~~~
bigslice --help | head -n20
~~~
{: .bash}

~~~
usage: bigslice [-i <folder_path>] [--resume] [--complete] [--threshold T]
                [--threshold_pct <N>] [--query <folder_path>]
                [--query_name <name>] [--run_id <id>] [--n_ranks N_RANKS]
                [-t <N>] [--hmmscan_chunk_size <N>] [--subpfam_chunk_size <N>]
                [--extraction_chunk_size EXTRACTION_CHUNK_SIZE] [--scratch]
                [-h] [--program_db_folder PROGRAM_DB_FOLDER] [--version]
                <output_folder_path>

                            _________
 ___    _____|\____|\____|\ \____    \
|   \  |       }     }     }  ___)_ _/__
| >  | _--/--|/----|/----|/__/  __||  __|
|   < | ||  __/ (  (| | \___/  /__/|  _|
| >  || || |_ | _)  ) |_ | |\  \__ | |__
|____/|_| \___/|___/|___||_| \____||____| [ Version 1.1.0 ]

Biosynthetic Gene clusters - Super Linear Clustering Engine
(https://github.com/medema-group/bigslice)

positional arguments:
~~~
{: .output}

`BiGSLICE` is asking for a folder as the input. First, it is 
important to highlight that the bones of this folder are the BGCs 
from a group of genomes that has been obtained by `AntiSMASH`. In its [GitHub](https://github.com/medema-group/bigslice) page, we can search for 
an input folder [template](https://github.com/medema-group/bigslice/tree/master/misc/input_folder_template). The folder needs three 
main components:

- **datasets.tsv:** This is a file that **needs to have this exact name**. This must be a tabular separated file where the information of 
each dataset (BGCs from a group of genomes) must be specified.

<a href="../fig/02-05-03.png">
  <img src="../fig/01-05-03.png" alt="Aquí va el texto que describe a la imagen." />
</a>


- **dataset_n:** Each dataset will be composed by the BGCs of different 
genomes. We can give `BiGSLICE` **n** groups of BGCs. The separation 
of the BGCs in different datasets is due to the different 
characteristics that the bacterial lineages can have. For example, if 
we have a set of bacterial populations that came from maize roots and 
other ones that were obtained from tomato roots, we can put them into 
dataset_1 and dataset_2 respectively.

- **taxonomy_n.tsv:**This is also a tabular separated file that will 
carry the taxonomix information of each of the genomes where the 
input BGCs were found and the path to reach these BGCs inside the 
input-folder:
	1. Genome folder name (ends with '/')
	2. Kingdom / Domain name
	3. Class name
	4. Order name
	5. Family name
	6. Genus name
	7. Species name
	8. Organism / Strain name


Here, we have an example of the structure of the `input-folder`:

<a href="../fig/02-05-04.png">
  <img src="../fig/01-05-04.png" alt="Aquí va el texto que describe a la imagen." />
</a>

### Creating the input-folder

Now that we now what input `BiGSLICE` requires, we will do our 
input-folder step by step. First, let's remeber how much genomes 
we have:

~~~
$ ls -F ../antismash/output/
~~~
{: .bash}

~~~
Streptococcus_agalactiae_18RS21/  Streptococcus_agalactiae_A909/    Streptococcus_agalactiae_COH1/
Streptococcus_agalactiae_515/     Streptococcus_agalactiae_CJB111/  Streptococcus_agalactiae_H36B/
~~~
{: .output}

We have six _Streptococcus_ genomes from the original papar, and -- 
public genomes. We will allocate their respective BGC `.gbk`s in 
two `dataset`s, one for the genomes from Tettelin _et al._ paper, and 
the another for the public ones.

After corroborating that we are on the `bigslice` folder, we will 
begin the construction of the input.

~~~
$ mkdir input-folder
$ mkdir input-folder/dataset_1
$ mkdir input-folder/dataset_2
$ mkdir taxonomy
$ tree
~~~
{: .bash}

~~~
.
└── input-folder
    ├── dataset_1
    ├── dataset_2
    └── taxonomy

4 directories, 0 files
~~~
{: .output}

Now we will create the folders for the BGCs of the dataset_1 genomes. 
We will take advantage on the strain name of our _Streptococcus agalactiae_ lineajes to create their folders:

~~~
$ for i in 18RS21 COH1 515 H36B A909 CJB111; 
  do mkdir input-folder/dataset_1/Streptococcus_agalactiae_$i;
  done
$ tree -F
~~~
{: .bash}

~~~
.
└── input-folder/
    ├── dataset_1/
    │   ├── Streptococcus_agalactiae_18RS21/
    │   ├── Streptococcus_agalactiae_515/
    │   ├── Streptococcus_agalactiae_A909/
    │   ├── Streptococcus_agalactiae_CJB111/
    │   ├── Streptococcus_agalactiae_COH1/
    │   └── Streptococcus_agalactiae_H36B/
    ├── dataset_2/
    └── taxonomy/

10 directories, 0 files
~~~
{: .output}

We will do the same for the public genomes:
~~~
$ for i in -- --; 
  do mkdir input-folder/dataset_2/Streptococcus_agalactiae_$i;
  done
$ tree -F
~~~
{: .bash}

~~~
--
--
--
--
--
--
--
--
--
~~~
{: .bash}

Next, we will copy the BGCs `.gbk` files from the dataset_1 
genomes from each `AntiSMASH` output directory to its respective 
folder .

~~~
$ ls input-folder/dataset_1/ | while read line;
  do cp ../antismash/output/$line/*region*.gbk input-folder/dataset_1/$line; 
  done
$ tree -F
~~~
{: .bash}

~~~
.
└── input-folder/
    ├── dataset_1/
    │   ├── Streptococcus_agalactiae_18RS21/
    │   │   ├── AAJO01000016.1.region001.gbk*
    │   │   ├── AAJO01000043.1.region001.gbk*
    │   │   └── AAJO01000226.1.region001.gbk*
    │   ├── Streptococcus_agalactiae_515/
    │   │   ├── AAJP01000027.1.region001.gbk*
    │   │   └── AAJP01000037.1.region001.gbk*
    │   ├── Streptococcus_agalactiae_A909/
    │   │   ├── CP000114.1.region001.gbk*
    │   │   └── CP000114.1.region002.gbk*
    │   ├── Streptococcus_agalactiae_CJB111/
    │   │   ├── AAJQ01000010.1.region001.gbk*
    │   │   └── AAJQ01000025.1.region001.gbk*
    │   ├── Streptococcus_agalactiae_COH1/
    │   │   ├── AAJR01000002.1.region001.gbk*
    │   │   └── AAJR01000044.1.region001.gbk*
    │   └── Streptococcus_agalactiae_H36B/
    │       ├── AAJS01000020.1.region001.gbk*
    │       └── AAJS01000117.1.region001.gbk*
    ├── dataset_2/
    └── taxonomy/

10 directories, 13 files
~~~
{: .output}

Again, we will do the same for the BGCs `.gbk`s of the dataset_2:
~~~
$ ls input-folder/dataset_2/ | while read line;
  do cp ../antismash/output/$line/*region*.gbk input-folder/dataset_2/$line; 
  done
$ tree -F
~~~
{: .bash}

~~~
--
---
--
--
--
--
--
~~~
{: .bash}

> ## Exercise 1.
> As we have seen, the structure of the input folder for BiGSLICE is quite difficult to get. Imagine "Sekiro" wants to copy the directory structure to use it for future BigSlice inputs.
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


#### datasets.tsv file - The silmaril of BiGSLICE

The next step is to create the main file **datasets.tsv**. First we 
put the first lines to this file. In each of these `.tsv` files, we 
can put lines that begin with `#`. This will not be read it by the 
code, and it can be of help to know whit information is located 
in those files. We will use the command `echo` with the `-e` flag 
that will enable us to put tab separations between the text:

~~~
$ cd input-folder
$ echo -e "#Dataset name""\t""Path to folder""\t""Path to taxonomy""\t""Description" > datasets.tsv
$ more datasets.tsv

~~~
{: .bash}

~~~
#Dataset name   Path to folder  Path to taxonomy        Description
~~~
{: .output}

We will use `echo` *One more time* to put the information of out two 
datasets. But this time, we will indicate bash that we want to insert 
this new line in the existing `datasets.tsv` with the `>>` option.

~~~
$ echo -e "dataset_1""\t""dataset_1/""\t""taxonomy/dataset_1_taxonomy.tsv""\t""Tetteling genomes" >> datasets.tsv
$ echo -e "dataset_2""\t""dataset_2/""\t""taxonomy/dataset_2_taxonomy.tsv""\t""Public genomes" >> datasets.tsv
$ more datasets.tsv
~~~
{: .bash}

~~~
#Dataset name   Path to folder  Path to taxonomy        Description
dataset_1       dataset_1/      taxonomy/dataset_1_taxonomy.tsv Tetteling genomes
dataset_2       dataset_2/      taxonomy/dataset_2_taxonomy.tsv Public genomes
~~~
{: .output}

The main file of the input-folder is finished!

#### The taxonomy of the input-folder

We also need to specify the taxonomic assignation of each of the 
intup genomes BGC's. We will build one `dataset_taxonomy.tsv` file 
for each one of our datasets, _i.e._ two in total. First, let's create 
the header of each one of these files using `echo`:

~~~
$ echo -e "#Genomefolder""\t"Kingdom"\t"Phylum"\t"Class"\t"Order"\t"Family"\t"Genus"\t""Species Organism" > taxonomy/dataset_1_taxonomy.tsv
$ echo -e "#Genomefolder""\t"Kingdom"\t"Phylum"\t"Class"\t"Order"\t"Family"\t"Genus"\t""Species Organism" > taxonomy/dataset_2_taxonomy.tsv
$ more taxonomy/taxonomy/dataset_1_taxonomy.tsv
~~~
{: .bash}

~~~
#Genome folder  Kingdom Phylum  Class   Order   Family  Genus   Species Organism
~~~
{: .output}

There are several ways to obtain the taxonomic data. One of them is 
searching for each lineage taxonomic identification on [NCBI](https://www.ncbi.nlm.nih.gov/guide/taxonomy/). There is also a way to get this information from our `.gbk` files:

~~~
$ head -n20 ../../annotated/Streptococcus_agalactiae_18RS21.gbk
~~~
{: .bash}

~~~
LOCUS       AAJO01000169.1          2501 bp    DNA     linear   UNK
DEFINITION  Streptococcus agalactiae 18RS21
ACCESSION   AAJO01000169.1
KEYWORDS    .
SOURCE      Streptococcus agalactiae 18RS21.
  ORGANISM  Streptococcus agalactiae 18RS21
            Bacteria; Terrabacteria group; Firmicutes; Bacilli;
            Lactobacillales; Streptococcaceae; Streptococcus; Streptococcus
            agalactiae.
FEATURES             Location/Qualifiers
     source          1..2501
                     /mol_type="genomic DNA"
                     /db_xref="taxon:342613"
                     /genome_md5=""
                     /project="nselem35_342613"
                     /genome_id="342613.37"
                     /organism="Streptococcus agalactiae 18RS21"
     CDS             1..213
                     /db_xref="SEED:fig|342613.37.peg.1973"
                     /db_xref="GO:0003735"
~~~
{: .output}

We will use again `echo` to write this information into our 
`dataset_taxonomy.tsv`. This is going to be a little long because 
we have 8 genomes adn we will need to write 8 `echo` lines, but 
bear with us. We are almost there!

~~~
$ echo -e "Streptococcus_agalactiae_18RS21/""\t"Bacteria"\t"Firmicutes"\t"Bacilli"\t"Lactobacillales"\t"Streptococcaceae"\t"Streptococcus"\t""Streptococcus agalactiae 18RS21" >> taxonomy/dataset_1_taxonomy.tsv

$ echo -e "Streptococcus_agalactiae_515/""\t"Bacteria"\t"Firmicutes"\t"Bacilli"\t"Lactobacillales"\t"Streptococcaceae"\t"Streptococcus"\t""Streptococcus agalactiae 515" >> taxonomy/dataset_1_taxonomy.tsv

$ echo -e "Streptococcus_agalactiae_A909/""\t"Bacteria"\t"Firmicutes"\t"Bacilli"\t"Lactobacillales"\t"Streptococcaceae"\t"Streptococcus"\t""Streptococcus agalactiae A909" >> taxonomy/dataset_1_taxonomy.tsv

$ echo -e "Streptococcus_agalactiae_CJB111/""\t"Bacteria"\t"Firmicutes"\t"Bacilli"\t"Lactobacillales"\t"Streptococcaceae"\t"Streptococcus"\t""Streptococcus agalactiae CJB111" >> taxonomy/dataset_1_taxonomy.tsv

$ echo -e "Streptococcus_agalactiae_COH1/""\t"Bacteria"\t"Firmicutes"\t"Bacilli"\t"Lactobacillales"\t"Streptococcaceae"\t"Streptococcus"\t""Streptococcus agalactiae COH1" >> taxonomy/dataset_1_taxonomy.tsv

$ echo -e "Streptococcus_agalactiae_H36B/""\t"Bacteria"\t"Firmicutes"\t"Bacilli"\t"Lactobacillales"\t"Streptococcaceae"\t"Streptococcus"\t""Streptococcus agalactiae H36B" >> taxonomy/dataset_1_taxonomy.tsv

$ more taxonomy/dataset_1_taxonomy.tsv
~~~
{: .bash}
~~~
#Genome folder   Kingdom Phylum  Class   Order   Family  Genus   Species Organism
Streptococcus_agalactiae_18RS21/        Bacteria        Firmicutes      Bacilli Lactobacillales Strept
ococcaceae      Streptococcus   Streptococcus agalactiae 18RS21
Streptococcus_agalactiae_515/   Bacteria        Firmicutes      Bacilli Lactobacillales Streptococcace
ae      Streptococcus   Streptococcus agalactiae 515
Streptococcus_agalactiae_A909/  Bacteria        Firmicutes      Bacilli Lactobacillales Streptococcace
ae      Streptococcus   Streptococcus agalactiae A909
Streptococcus_agalactiae_CJB111/        Bacteria        Firmicutes      Bacilli Lactobacillales Strept
ococcaceae      Streptococcus   Streptococcus agalactiae CJB111
Streptococcus_agalactiae_COH1/  Bacteria        Firmicutes      Bacilli Lactobacillales Streptococcace
ae      Streptococcus   Streptococcus agalactiae COH1
Streptococcus_agalactiae_H36B/  Bacteria        Firmicutes      Bacilli Lactobacillales Streptococcace
ae      Streptococcus   Streptococcus agalactiae H36B
~~~
{: .output}

We will do the same for the `dataset_2_taxonomy.tsv` file:

~~~
--
--
--
--
--
--
~~~
{: .bash}
~~~
--
--
--
--
--
--
--
~~~
{: .output}

Now, we have the organization of our `input-folder` complete
~~~
tree -F input_folder/
~~~
{: .bash}

~~~
input_folder/
├── dataset_1/
│   ├── Streptococcus_agalactiae_18RS21/
│   │   ├── AAJO01000016.1.region001.gbk
│   │   ├── AAJO01000043.1.region001.gbk
│   │   └── AAJO01000226.1.region001.gbk
│   ├── Streptococcus_agalactiae_515/
│   │   ├── AAJP01000027.1.region001.gbk
│   │   └── AAJP01000037.1.region001.gbk
│   ├── Streptococcus_agalactiae_A909/
│   │   ├── CP000114.1.region001.gbk
│   │   └── CP000114.1.region002.gbk
│   ├── Streptococcus_agalactiae_CJB111/
│   │   ├── AAJQ01000010.1.region001.gbk
│   │   └── AAJQ01000025.1.region001.gbk
│   ├── Streptococcus_agalactiae_COH1/
│   │   ├── AAJR01000002.1.region001.gbk
│   │   └── AAJR01000044.1.region001.gbk
│   └── Streptococcus_agalactiae_H36B/
│       ├── AAJS01000020.1.region001.gbk
│       └── AAJS01000117.1.region001.gbk
├── dataset_2/
│   └── Streptococcus_agalactiae_GBS_M002/
│       ├── CP013908.1.region001.gbk
│       └── CP013908.1.region002.gbk
├── datasets.tsv
└── taxonomy/
    ├── dataset_1_taxonomy.tsv
    └── dataset_2_taxonomy.tsv

10 directories, 18 files
~~~
{: .output}


> ## Exercise 2 
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

### Running BiGSLICE

~~~

~~~
{: .bash}

~~~

~~~
{: .bash}

> ## Discussion
> Considering the results in the runs tab, we can see that there are a lot of Gene Cluster Families that have only one cluster associated to it (GCF_1, GCF_2, GCF_5, GCF_7). <br>
> What does this tell us about the metabolites diversity of the Streptococcus sample?
> > ## Solution
> > We can see that there are some unique gene cluster families, which mean that there are some organism that has that unique gene cluster and therefore he has some metabolite that the others don´t and that may help him in his environmente. So, as there are many singleton Gene Cluster Families, we can say that theres a big diversity from the sample because many of the organisms in the sample have unique "habilities" (metabolites).
> {: .solution}
{: .discussion}   


> ## Discussion
> Suppose we get the following results from a sample of 6 organisms.
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
>  What can we infer about the metabolite diversity?
{: .discussion}  




## BiG-FAM 

{% include links.md %}

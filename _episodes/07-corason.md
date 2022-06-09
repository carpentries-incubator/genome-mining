---
title: "Finding variation on genomic vicinities"
teaching: 30
exercises: 30
questions:
- "How can I follow variation in genomic vicinities given a reference BGC?"
- "Which gene families are the conserved part of a BGC family?"
objectives:
- "Learn to find BGC-families "
- "Visualize variation in a genomic vicinity"
keypoints:
- "CORASON is a command-line tool that finds BGC-families"
- "Genomic vicinity variation is organized phylogenetically according to the conserved genes in the BGC-family"
---

CORASON is a visual tool that identifies gene clusters that share a 
common genomic core and reconstructs multi-locus phylogenies of these 
gene clusters to explore their evolutionary relationships. CORASON 
was developed to find and prioritize biosynthetic gene clusters 
(BGC), but can be used for any kind of clusters.

Input: query gene, reference BGC and genome database.
Output: SVG figure with BGC in the family sorted according 
to the multi-locus phylogeny of the core genes.

Advantages  
- SVG graphs Scalable graphs that allows metadata easy display.  
- Interactive CORASON is not a static database, it allows you to explore your own genomes.  
- Reproducibility CORASON runs on docker and conda, 
this containerization which allows to always perform the same analysis 
even if you change your Linux/perl/blast/muscle/Gblocks/quicktree local distributions.  

## CORASON conda 
Here we are testing the new stand-alone 
[corason in a conda environment](https://github.com/miguel-mx/corason-conda)
with gbk as input-files. Lets first activate the corason-conda environment.    

~~~
conda activate corason  
~~~
{: bash}

~~~
(corason) user@server:~$
~~~
{: .output}

With the environment activated all CORASON-dependencies are ready to be used. 
The next step is to clone CORASON-software from its GitHub repository. First,
place yourself at the results directory and then clone CORASON-code.
~~~
~/dc_workshop/results/genome-mining 
git clone https://github.com/miguel-mx/corason-conda.git 
ls
~~~
{: bash}

The GitHub CORASON repository must be now in your directory. 
~~~
corason-conda 
~~~
{: .output}

CORASON was written to be used with RAST annotation as input files, in this case
we are using a genome database composed of `.gbk` files. So, we first need to convert
gbk files into a CORASON-compatibles input files.  
~~~
cd corason-conda/EXAMPLE2      
mkdir  CORASON_GENOMES
cp   ~/dc_workshop/results/annotated/*gbk CORASON_GENOMES
~~~
{: .code}
 
Here the reference protein is cpsG, whose encoding gene is part of the [polysaccharide BGC](https://mibig.secondarymetabolites.org/repository/BGC0000744/index.html#r1c1) produced by some _S. agalactie_   

~~~
../CORASON/corason.pl -q cpsg.query -gbk -s GBKS/agalactiae_COH1_prokka.gbk 
~~~
{: bash}

~~~
mv output/* . 
ls
~~~
{: bash}  

~~~
test
~~~
{: .output}  


Now we will run CORASON with cpsg.query over all _S. galactiae_ genomes.  
~~~
../CORASON/corason.pl -q cpsg.query -s 100006  -rast_ids Corason_Rast.IDs`
~~~
{: bash}

Finally, we have all the genomic vicinities sorted phylogenetically according to 
the genes in the core-cluster. We can download the resulting svg file to our local computer.
~~~
scp (remoto)/corason-conda/EXAMPLE2/output/cpsg.query-output  Downloads/.
~~~
{: bash}


{% include links.md %}

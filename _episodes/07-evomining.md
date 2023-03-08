---
title: "Evolutionary Genome Mining"
teaching: 20
exercises: 20
questions:
- "What is Evolutionary Genome Mining?"
- "Which kind of BGCs can EvoMining find?"
- "What do I need in order to run an evolutionary genome mining analysis?"
objectives:
- "Understand EvoMining pipeline."
- "Run an example of evolutionary analysis in cpsG gene family."
- "Explore MicroReact interactive output interface."
keypoints:
- "EvoMining is a command-line tool that performs evolutionary genome mining over gene families"
- "EvoMining hits can belong to new BGC"
- "MicroReact is an interactive genomic visualizer compatible with EvoMining output"
---
{% include links.md %}

<a href="../fig/evomining.gif">
  <img src="../fig/evomining.gif" alt="a) EvoMining expansion-and-recruitment pipeline. A group of grey stacked cylinders representing genomes in a database (DB).
                                   	Homologues and expansions of seed enzymes, represented as an orange arrow, from the enzyme DB
                                   	are searched by blastp in the genome DB.
                                   	The outcome is integrated as the expanded enzyme families (EFs) within the genome DB.
                                   	Bidirectional best hits (BBH) of seed enzymes, red arrows, are marked as conserved metabolism.
                                   	The EFs are amplified after being compared against a DB of natural products (NP) biosynthetic enzymes,
                                   	represented by a blue cylinder, to find recruitments defined as enzymes of the family that are part of a MIBiG BGC.
                                   	b) The genome DB, represented by the gray stacked cylinders, is searched as previously described.
                                   	Additionally, antiSMASH predictions, cyan arrows, can be added by the user.
                                   	antiSMASH enzyme predictions that are at the same time marked in red are defined as transition enzymes, purple arrows.
                                   	c) EvoMining phylogenetic reconstruction and visualization. On the left side, a phylogenetic reconstruction of an EF is shown.
                                   	On the right side it is shown the EvoMining tree displaying the EvoMining predictions (green),
                                   	which are those extra copies closer to enzyme recruitments into BGC (blue) than to conserved metabolic enzymes (red).
                                   	antiSMASH predicted enzymes are represented in cyan, transition enzymes in black and
                                   	extra copies that are neither antiSMASH nor EvoMining predictions are left in grey." />
</a>

 Usually, bioinformatics tools related to the prediction of Natural Products (NP)
 biosynthetic genes try to find metabolic pathways of enzymes that are known to be
 related with the synthesis of secondary metabolites. However, these approaches
 fail for the discovery of novel biosynthetic systems. Thus,
 [EvoMining](https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000260) tries to circumvent this problem by detecting novel enzymes that may be implicated in the synthesis of new natural products in Bacteria.
 
 To know more about EvoMining you can read [Selem et al, Microbial Genomics 2019](https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000260).   
 
EvoMining searches protein expansions that may have evolved from the conserved
metabolism into a specialized metabolism. It builds phylogenetic
trees based on all the protein copies of a certain enzyme in a given genome
database. The output tree differentiates copies that are related with the
conserved metabolism, copies that are known to be implicated in discovered
NP-producing-BGCs i.e. BGCs from [MiBIG database](https://mibig.secondarymetabolites.org/)
and, optionally, protein copies that belong to BGCs predicted by
[antiSMASH](https://antismash-db.secondarymetabolites.org/). Finally,
some branch in the tree will be depicted as "EvoMining hits", which represent
enzyme expansions that are evolutionary closer to those copies related with
the secondary metabolism (MiBIG or antiSMASH BGCs) than to those related with
the conserved (primary) metabolism.

## Run evomining image

First, place yourself at your working directory.
~~~
$ cd   ~/gm_workshop/results/genome-mining/corason-conda/EXAMPLE2  
$ ls
~~~
{: .language-bash}
~~~
CORASON_GENOMES  Corason_Rast.IDs  cpsg.query  GENOMES  output
~~~
{: .output}  

The general structure of a docker container is shown in the next bash-box. Note that
it requires to specify which docker container will run. Optionally,
with `-v` flag it is possible to share a directory with the container,
with `-p` flag a port is shared and it is also possible to specify which
program will run inside the container.  
~~~
$ docker run --rm -i -t -v <your local directory>:<inside docker directory> -p <inside port>:80 <docker container> <program inside docker>    
~~~
{: .language-bash}   

EvoMining is inside a docker container, so the general structure
to start your analysis will be as follows:   
~~~
$ docker run --rm -i -t -v $(pwd):/var/www/html/EvoMining/exchange -p 8080:80 nselem/evomining:latest /bin/bash   
~~~
{: .language-bash}   

Let's explain the pieces of this line.   
 
| command  |                             	Explanation                                        	|    
|:-------:|----------------------------------------------------------------------------------------|    
|docker   | tells the system that we are running a docker command                               	|    
| run 	|  the command that we are running is to run a docker container                      	|    
| --rm	|  this container will be removed after closed                                       	|    
| -i  	|  this container allows user interaction                                            	|    
| -t  	|  this interaction will be through a terminal                                       	|   
| -v  	| a data volume (directory) will be shared between your local machine and the container  |    
| -p  	|  a port will allow a web based app                                                 	|   	 

However, sometimes the port 80 is busy, in that case you can
use other ports like 8080 or 8084. If this is the case, please use the port `80X`
where X is a number between 01..30 provided by your instructor.   
```
$ docker run --rm -i -t -v $(pwd):/var/www/html/EvoMining/exchange -p 8080:80 nselem/evomining:latest /bin/bash  
$ docker run --rm -i -t -v $(pwd):/var/www/html/EvoMining/exchange -p 8084:80 nselem/evomining:latest /bin/bash  
```

If your docker container worked, now you will see in your terminal
a new prompt. Instead of the usual dollar sign, there should be a number
`#` at the beginning of your terminal. This is because now you are inside
the docker container and you have `sudo` permissions inside the docker.  
~~~
#  
~~~
{: .language-bash}

To exit container use `exit`  
~~~
# exit
~~~
{: .language-bash}  
 
And now your prompt must be back in the dollar sign  
~~~
$   
~~~
{: .language-bash}  


To see the running container use `ps`  
~~~
$ docker ps
~~~
{: .language-bash}  

~~~
2f879ba6e337   nselem/evomining:latest   "/bin/bash"   11 hours ago   Up 11 hours   0.0.0.0:8014->80/tcp, :::8014->80/tcp   relaxed_dirac
~~~
{: .output}

To stop the running container use `docker stop` and to remove them use `docker rm`  
~~~
$ docker stop relaxed_dirac  
$ docker remove relaxed_dirac  
~~~
{: .language-bash}  

~~~
2f879ba6e337
~~~
{: .output}

## Set EvoMining genomic database
Start the container again with your corresponding port.  
~~~
$ docker run --rm -i -t -v $(pwd):/var/www/html/EvoMining/exchange -p 80X:80 nselem/evomining:latest /bin/bash   
~~~
{: .language-bash}   

Though we will NOT run the test EvoMining command, it looks as follows:
~~~
# perl startEvoMining.pl  
~~~
{: .code}
 
Instead of that, customize the genomic database by using the same as CORASON.  
Notice that EvoMining requires RAST-like annotated genomes and for this reason
we are using the fasta files that CORASON converts from our gbk inputs.
~~~
# perl startEvoMining.pl -g GENOMES -r  Corason_Rast.IDs
~~~
{: .code}  

<a href="../fig/tree.png">
  <img src="../fig/tree.png" alt="EvoMining phylogenetic reconstruction providing evolutionary insights into the metabolic origin
                              	and the fate of members of diverse EF from the Streptococcus example.
                              	Seed enzymes are labeled in orange. The most conserved copies or central metabolism copies are marked in red.
                              	Enzyme copies recruited into specialized metabolism, contained in MIBiG, are labeled in blue.
                              	Enzyme copies that are closer to blue enzyme recruitments than to red conserved enzymes are labeled in green
                              	and represent EvoMining Hits. Extra copies with an unknown metabolic fate are shown in gray." />
</a>

Finally, remember that `X` means your user-number and open your browser
at the address: `http://132.248.196.38:80X/EvoMining/html/index.html`. Once there,
just click the start button and enjoy!

When you finish using this container, please exit it.
~~~
#exit
~~~
{: .code}    

## Set the conserved-enzymes database

When using EvoMining, oftenly you will desire to construct your own conserved enzymes database.
To know more about how to configure a database, consult the EvoMining wiki
in the [EvoMining databases](https://github.com/nselem/evomining/wiki/Databases-Conformation) part.
Natural products database could also be replaced for another set of
genes that are "true positives", for example a set of regulatory genes.

As an example, transform the file `cpsg.query` into the format of this database.
This file contains the aminoacid sequence of the _cpsG_ gene. Firstly, copy this file
into what will become the conserved-enzymes database.  
~~~
$ cp cpsg.query cpsg_cdb
~~~
{: .language-bash}

Now, it requires some editing. Open nano editor and change the first line `>cpsg` to
`>SYSTEM1|1|phosphomannomutase|Saga `. EvoMining conserved-database needs a
four-field format pipe-separated that contains; the name of the metabolic system to which the
enzyme belongs (SYSTEM1), a consecutive number of the enzyme (1 in this case),
the function of the enzyme, and finally, an abbreviation of the organism Saga, (_S. Agalactiae_).  
The reason behind this is that this was the way we needed EvoMining for its first use and we have not changed the headers since.  
~~~
$ nano cpsg_cdb
~~~
{: .language-bash}  

~~~

~~~
{: .language-bash}  

Run your EvoMining docker
~~~
$ docker run --rm -i -t -v $(pwd):/var/www/html/EvoMining/exchange -p 80X:80 nselem/evomining:latest /bin/bash   
~~~
{: .language-bash}   

and inside this new container:
~~~
# perl startEvoMining.pl -g GENOMES -r  Corason_Rast.IDs -c cpsg_cdb
~~~
{: .code}

Use the website again and think about the results.

> ## Exercise 1. Set EvoMining parameters    
> Complete the blanks in the following EvoMining run:
>   `actinoSMASH` A file with the ids of antiSMASH recognized genes.
>   `Actinos`  a directory with RAST-like fasta and annotation files.
>   `Histidine-db` A fasta file with some proteins in the histidine pathway.  
>   `Actinos.ids` tabular files with the RAST ids and the name of the organisms.
>   
> ~~~
>  # perl starEvoMining.pl -g ____ -c _____ -r _____ -a ___________  
> ~~~
> >{: .code}
>
>
> > ## Solution
> >
> > ~~~
> > # perl starEvoMining.pl -g Actinos -c Histidine-db -r Actinos.ids -a actinoSMASH  
> > ~~~
> > Actinos is the genomic database, Histidine-db is the conserved-enzymes database,
> > Actinos.ids is the file that relates Rast ids with the organisms names, and actinoSMASH
> > contains the genes identified by antiSMASH.  
> >
> > {: .laguage-bash}
> {: .solution}
{: .challenge}  

> ## Discussion 1. Retro EvoMining in enzyme database
>
> What do you learn from running in a conserved-enzymes database the gene _cpsG_ that is part of a specialized BGC?
>
> > ## Solution
> >  _cpsG_ does not have extra copies in Streptococcus agalactiae, so there are no expansions that may be functional divergent.
> >  _cpsG_ single copies in the genomes look red-colored in EvoMining output, as if they belong to the conserved-metabolism.
> >   However, this is not the case, the color is because there is only one copy and it is merged into MIBiG true-positives because it was
> >   originally a gene in the specialized metabolism. So it is important to know the seed enzymes.  
> >
> {: .solution}
{: .discussion}

## Visualize your results in MicroReact  

Firstly, you have to run all the pipeline in the website:
http://<yourip>/EvoMining/html/index.html, and then all the
output files will be generated. You can use the EvoMining
basic interface or take your results into MicroReact.  

EvoMining outputs are stored in the directory `<conserved-db>_<natural-db>_<genomes-db>`  
~~~
$ ls
~~~
{: .language-bash}

~~~
cpsg_cdb_MiBIG_DB.faa_GENOMES
~~~
{: .output}
 
```
scp betterlab@132.248.196.38:~/dc_workshop/results/genome-mining/corason-conda/EXAMPLE2/ALL_curado.fasta_MiBIG_DB.faa_GENOMES/blast/seqf/tree/1.tree ~/Downloads/.
scp betterlab@132.248.196.38:~/dc_workshop/results/genome-mining/corason-conda/EXAMPLE2/ALL_curado.fasta_MiBIG_DB.faa_GENOMES/blast/seqf/tree/1.csv ~/Downloads  
```
 
To explore EvoMining outputs, upload 1.nwk and 1.csv
files to [microReact](https://microreact.org/).  
Here you can find the [MicroReact visualization](https://microreact.org/project/e8b7wWZkovtavPFFpBXRPp-evomining-streptococcus-example)
of this EvoMining run.  

<a href="../fig/EvoMiningMicroReact.png">
  <img src="../fig/EvoMiningMicroReact.png" alt="MicroReact visualization of the EvoMining run Streptococcus example.
                                             	At the left a bar-chart with the EF in the X axis and the number of entries in the Y axis.
                                             	At the right, the EvoMining phylogenetic tree using the same color code as the chart.
                                             	Right of the tree the legend indicating the colors by metabolism; central metabolism enzymes in red,
                                             	expansion enzymes in gray, recruited enzymes contained in MIBiG in blue,
                                             	secondary metabolism enzymes (EvoMining hits) are marked in green,
                                             	and seed enzymes are colored in orange. Below appears the metadata from the run,
                                             	organized in a five row table including Id, metabolism, genome, function and copies." />
</a>
 
## Other resources    
To run EvoMining with a larger conserved-metabolite DB you can use
[EvoMining Zenodo](https://zenodo.org/record/1219709#.YqEsFqjMLrc) data.

To explore more EvoMining options, please explore [EvoMining wiki](https://github.com/nselem/evomining/wiki).

[ARTS](https://arts.ziemertlab.com/) is another evolutionary
genome mining software with its corresponding database
[ARTS-db](https://arts-db.ziemertlab.com/) .

> ## Evolutionary Genome Mining
> To learn more about Genome Mining you can read these references:
> - The confluence of big data and evolutionary genome mining for the discovery of natural products.
>   [Chevrette et al, 2021](https://doi.org/10.1039/D1NP00013F)`
> - Evolutionary Genome Mining for the Discovery and Engineering of Natural Product Biosynthesis.
> [Chevrette et al, 2022](https://doi.org/10.1007/978-1-0716-2273-5_8)
{: .callout}


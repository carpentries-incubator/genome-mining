---
title: "Evolutionary Genome Mining"
teaching: 20
exercises: 20
questions:
- "What is Evolutionary Genome Mining?"
- "Which kind of BGCs can EvoMining find?"
- "What do I need to run an evolutionary genome mining analysis?"
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
  <img src="../fig/evomining.gif" alt="Aquí va el texto que describe a la imagen." />
</a>

 Usually, bioinformatics tools related to the prediction of Natural Products (NP) 
 biosynthetic genes try to find metabolic pathways of enzymes that are known to be 
 related with the synthesis of a secondary metabolites. However, these approaches 
 fail for the discovery of novel biosynthetic systems. Thus, 
 [EvoMining](https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000260) try to solve this problem to detect novel enzymes that may be implicated in the synthesis of new natural products in Bacteria.
 
 To know more about EvoMining you can read [Selem et al, Microbial Genomics 2020](https://www.microbiologyresearch.org/content/journal/mgen/10.1099/mgen.0.000260).   
 
This tool looks for protein expansions that may have evolved from the central 
metabolism into a specialized metabolism. For that, it builds phylogenetic 
trees based on all the protein copies of a certain enzyme in a given genome 
database. The output tree will differentiate copies that are related with the 
central metabolism, copies that are known to be implicated in discovered 
NP-producing-BGCs i.e. BGCs from [MiBIG database](https://mibig.secondarymetabolites.org/)
and, optionally, protein copies that belong to BGCs predicted by
[antiSMASH](https://antismash-db.secondarymetabolites.org/). Finally, 
some branch in the tree will be depicted as "EvoMining hits", which represent 
enzyme expansions that are evolutionary closer to those copies related with 
the secondary metabolism (MiBIG or antiSMASH BGCs) than to those related with 
the central (primary) metabolism.

## Run evomining image

First, place yourself at your working directory.
~~~
$ cd   ~/dc_workshop/results/genome-mining/corason-conda/EXAMPLE2  
$ ls
~~~
{: .language-bash}
~~~ 
CORASON_GENOMES  Corason_Rast.IDs  cpsg.query  GENOMES  output 
~~~
{: .output}  

The general structure of a docker container is shown in the next bash-box. Note that
it requires to specify which docker containerwill be run. Opcionally
with `-v` flag it is posible to share a directory with the container,
with `-p` flag a port is shared and it is also posible to specify which
program will be run inside the container.  
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

Lets explain the pieces of this line.  
| comand   | explanation   |  
|---|---|  
|docker   | tells the system that we are runing a docker command  |  
| run  |  the command that we are running is to run a docker container |  
| --rm  |  this container will be removed after closed  |  
| -i  |  this container allows user interaction  |  
|  -t |  this interaction will be trhough a terminal | 
| --v  | a data volume (directory) will be shared between your local machine and the container  |  
|  -p |  a port will allow a web based app|   

However, sometimes the port 80 is bussy, on that case you can 
use other ports like 8080 or 8084. In this case, please use the port `80X` 
where X is a number between 01..30 provided by your instructor.   
```
$ docker run --rm -i -t -v $(pwd):/var/www/html/EvoMining/exchange -p 8080:80 nselem/evomining:latest /bin/bash  
$ docker run --rm -i -t -v $(pwd):/var/www/html/EvoMining/exchange -p 8084:80 nselem/evomining:latest /bin/bash  
```

If your docker container worked, now you will see in your terminal
a new prompt. Instead of the usual dollar sign, now there is a number
`#` at the beggining of your terminal. This is because now you are inside
the docker container and you have `sudo` permisions inside the docker.  
~~~
#  
~~~
{: .language-bash}

To exit container use `exit`  
~~~ 
# exit
~~~ 
{: .language-bash}  
  
And now your prompt must be back in the dolar sign  
~~~ 
# 
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
$docker remove relaxed_dirac
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

Though we will NOT run the test EvoMining command, it will look as follows:
~~~
# perl startEvoMining.pl  
~~~
{: .language-bash}
  
Instead of that, lets customize our genomic database by using the same as CORASON.  
Note that EvoMining requires RAST-like annotated genomes and because of that 
we are using the fasta files that CORASON converts from our gbk inputs. 
~~~
# perl startEvoMining.pl -g GENOMES -r  Corason_Rast.IDs
~~~
{: .language-bash}  

<a href="../fig/tree.png">
  <img src="../fig/tree.png" alt="Aquí va el texto que describe a la imagen." />
</a>

## Visualize your results  

First you have to run all the pipeline in the website: 
http://<yourip>/EvoMining/html/index.html, and then all the 
 output files will be generated. You can use the EvoMining
  basic interface or take your results into MicroReact.  
  
```
scp betterlab@132.248.196.38:~/dc_workshop/results/genome-mining/corason-conda/EXAMPLE2/ALL_curado.fasta_MiBIG_DB.faa_GENOMES/blast/seqf/tree/1.tree ~/Downloads/.
scp betterlab@132.248.196.38:~/dc_workshop/results/genome-mining/corason-conda/EXAMPLE2/ALL_curado.fasta_MiBIG_DB.faa_GENOMES/blast/seqf/tree/1.csv ~/Downloads  
```
  
To explore EvoMining outputs upload 1.nwk and 1.csv 
files to [microReact](https://microreact.org/)  
Here is a [MicroReact visualization](https://microreact.org/project/e8b7wWZkovtavPFFpBXRPp-evomining-streptococcus-example) 
of this EvoMining run.  

<a href="../fig/EvoMiningMicroReact.png">
  <img src="../fig/EvoMiningMicroReact.png" alt="Aquí va el texto que describe a la imagen." />
</a>

## Set EvoMining protein database  
nano cpsg.query 
Discussion what happen in this case
Ans Is like a retro EvoMining 


> ## Discussion 1: Retro EvoMining in enzyme database
> 
> fixme
> 
> > ## Solution
> > 
> > fixme 
> {: .solution}
{: .discussion}

> ## Exercise 4 The size of a region.  
> Fixme
> 
>    
> ~~~
>  $ _____ fixme  
> ~~~
> >{: .laguage-bash}
> fixme
> 
> > ## Solution
> >
> > ~~~
> > $ fix
> > ~~~
> >fix
> > {: .laguage-bash}
> {: .solution}
{: .challenge}

## Other resources    
To run EvoMining with a biggest centralmetabolite DB you can use 
[EvoMining Zenodo](https://zenodo.org/record/1219709#.YqEsFqjMLrc) data.

To explore more EvoMining options, please explore [EvoMining wiki](https://github.com/nselem/evomining/wiki)

[ARTS](https://arts.ziemertlab.com/) is another evolutionary 
genome mining software with its corresponding database 
[ARTS-db](https://arts-db.ziemertlab.com/) . 

> ## Callout:Evolutionay Genome Mining
> To know more about Genome Mining you can read these references:
> - The confluence of big data and evolutionary genome mining for the discovery of natural products.
>   [Chevrette et al, 2021](https://doi.org/10.1039/D1NP00013F)`
> - Evolutionary Genome Mining for the Discovery and Engineering of Natural Product Biosynthesis. 
> [Chevrette et al, 2022](https://doi.org/10.1007/978-1-0716-2273-5_8)
{: .callout}

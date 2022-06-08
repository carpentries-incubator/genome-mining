---
title: "Evolutionary Genome Mining"
teaching: 20
exercises: 30
questions:
- "What is Evolutionary Genome Mining?"
- "Which kind of BGCs can EvoMining find?"
- "Which files extension accepts antiSMASH?"
objectives:
- "Understand how antiSMASH applications."
- "Understand the importance of metadata and potential metadata standards."
- "Explore common formatting challenges in spreadsheet data."
keypoints:
- "First key point. Brief Answer to questions. (antismash, genome mining, secondary metabolism, bacteria, bioactive coumpounds)"
---
{% include links.md %}

# EvoMining

## Introduction

 Usually, bioinformatics tools related to the prediction of Natural Products (NP) biosynthetic genes try to find metabolic pathways of enzymes that are known to be related with the synthesis of a secondary metabolites. However, these approaches fail for the discovery of novel biosynthetic systems. Thus, EvoMining try to solve this problem to detect novel enzymes that may be implicated in the synthesis of new natural products in Bacteria (_Referencia Evomining_).  
 
This tool looks for protein expansions that may have evolved from the central metabolism into a specialized metabolism. For that, it builds phylogenetic trees based on all the protein copies of a certain enzyme in a given genome database. The output tree will differentiate copies that are related with the central metabolism, copies that are known to be implicated in discovered NP-producing-BGCs (BGCs from MiBIG database (_Referencia MiBIG_)) and, optionally, protein copies that belong to BGCs predicted by antiSMASH. Finally, some branch in the tree will be depicted as "EvoMining hits", which represent enzyme expansions that are evolutionary closer to those copies related with the secondary metabolism (MiBIG or antiSMASH BGCs) than to those related with the central (primary) metabolism.

## Run evomining image

Place yourself at your working directory.
`cd   ~/dc_workshop/results/genome-mining/corason-conda/EXAMPLE2 `  

`ls `   
output:
 CORASON_GENOMES  Corason_Rast.IDs  cpsg.query  GENOMES  output 
 
 Run docker container  
`docker run --rm -i -t -v $(pwd):/var/www/html/EvoMining/exchange -p 8080:80 nselem/evomining:latest /bin/bash   `    
    
However, sometimes the port 80 is bussy, on that case you can use other ports like 8080 or 8084:    
`$ docker run --rm -i -t -v $(pwd):/var/www/html/EvoMining/exchange -p 8080:80 nselem/evomining:latest /bin/bash`  
`$ docker run --rm -i -t -v $(pwd):/var/www/html/EvoMining/exchange -p 8084:80 nselem/evomining:latest /bin/bash`  

perl startevominig

## Set EvoMining databases
`perl startevomining.pl -g GENOMES -r  Corason_Rast.IDs`

## GEtting results
>> scp betterlab@132.248.196.38:~/dc_workshop/results/genome-mining/corason-conda/EXAMPLE2/ALL_curado.fasta_MiBIG_DB.faa_GENOMES/seqf/blast/tree/1.tree ~/Downloads/.
>>
>> scp betterlab@132.248.196.38:~/dc_workshop/results/genome-mining/corason-conda/EXAMPLE2/ALL_curado.fasta_MiBIG_DB.faa_GENOMES/seqf/blast/tree/1.csv ~/Downloads  

To explore EvoMining outputs upload 1.tree and 1.csv files to [microReact](https://microreact.org/)  

To run EvoMining with a bigget centralmetabolite DB you can use Zenodo data.


---
title: "Introduction to genome Mining"
teaching: 10
exercises: 0
questions:
- "What is genome Mining?"
objectives:
- "Understand that Natural products are encoded in Biosynthetical Gene clusters"
- "Understand that Biosynthetical Gene clusters can be identified in the genomic material"
- "Discuss bioinformatic's good practices with you colleagues "

keypoints:
- "Natural products are encoded in Biosynthetical Gene Clusters"
---

Natural products are encoded in a Biosynthtetic gene clusters (BGCs) in Bacteria. 
Genome mining is the action of analyze genomes with specialized algorithms 
designed to find some BGCs. Some of these clusters were dilligently characterized 
by chemicals last century.Right now we have extensive databases that contains 
information about which genes belong to BGCs, and some control sets of genes that doesnt. 
Since the era of next generation sequencing, genomes have been explored 
as a source of discovering for new BGCs.

## Chloramphenicol a known antibiotic is produced in a BGC
<a href="{{ page.root }}/fig/episode1-fig1.PNG">
  <img src="{{ page.root }}/fig/episode1-fig1.PNG" alt="Cuatro Cienegas " />
</a>
[Explore the BGC](https://mibig.secondarymetabolites.org/repository/BGC0000893/index.html#r1c1)
## Starting a genome mining project

## Planning a Genome Mining project  
First, a set of genomes from taxa should be chosen. In this lesson
we will be working with _S. agalactiae_ genomes. This genus is not know
for its capabilities as a Natural products producer but is good enough
to show different approaches to genome mining. Recently metagenomes have been 
considered in genome mining studies. Here are some considerations 
taht may be useful for you as a genome miner: 

- Think about your research questions before start analyzing the data.  
- Remember, raw metadata should remain intact during all Genome Mining process.
It could be a good idea to change its file-permisions to read only.    
- Gather as much information in the form of metadata of 
all the genomes that you are working with.  
- All your intermediate steps should be considered temporal 
 and maybe removed without risk.   
- Save your scripts using a version manager, GitHub for example.
- Share your data in public repositories.   
- Give time to make your science repeatible, help your community.    




{% include links.md %}


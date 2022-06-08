---
title: "Finding variation on genomic vicinities"
teaching: 30
exercises: 30
questions:
- "How can I follow variation in genomic vicinities given a reference BGC?"
- "Which gene families are the conserved part of a BGC family?"
objectives:
- "Lear "
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---
FIXME

# CORASON
CORASON is a visual tool that identifies gene clusters that share a common genomic core and reconstructs multi-locus phylogenies of these gene clusters to explore their evolutionary relatioinships.

Input: query gene and RAST genome database.
Output: SVG graph with clusters sorted according to the multi-locus phylogeny of the common core.

CORASON was developed to find and prioritize biosynthetic gene clusters, but can be used for any kind of clusters.

Advantages
-SVG graphs Scalable graphs that allows metadata easy display.
-Interactive CORASON is not a static database, it allows you to explore your own genomes.
-Reproducibility CORASON runs on docker, which allows to always perform the same analysis even if you change your Linux/perl/blast/muscle/Gblocks/quicktree distributions.
## CORASON conda 
Here we are testing a new stand-alone [corason in a conda environment](https://github.com/miguel-mx/corason-conda)  
with gbk input-files
`conda activate corason`  
`git clone https://github.com/miguel-mx/corason-conda.git`    
`cd corason-conda/EXAMPLE2`      
`mkdir  CORASON_GENOMES`
`cp   ~/dc_workshop/results/annotated/*gbk CORASON_GENOMES`       
cpsG query from [polysaccharide BGC](https://mibig.secondarymetabolites.org/repository/BGC0000744/index.html#r1c1) 
`../CORASON/corason.pl -q cpsg.query -gbk -s GBKS/agalactiae_COH1_prokka.gbk `  
` mv output/* . `   
`../CORASON/corason.pl -q cpsg.query -s 100006  -rast_ids Corason_Rast.IDs`
`scp (remoto)/corason-conda/EXAMPLE2/output/cpsg.query-output  Downloads/.`


{% include links.md %}

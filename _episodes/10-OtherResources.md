---
title: "Other Resources"
teaching: 10
exercises: 10
questions:
- "Key question (FIXME)"
objectives:
- "First learning objective. (FIXME)"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---
## Other resources

We have seen how to carry on a genome mining project with some particular characteristics. However, each research project may need some deviations to these workflows. You may need to take use of RNA-Seq data, to search just for some specific domains instead of complete BGCs, or to combine metabolomics or proteomics with genomic data. Here we will provide a list of resources that are also useful for genome mining projects.

First, you can use some alternative program to search for BGCs in your genomes. The [Secondary Metabolite Bioinformatics Portal](https://www.secondarymetabolites.org/) list and introduce many diverse bioinformatic tools that pursue this goal. For example, CLUSEAN and NaPDoS allow to detect PKS and NRPS domains, while BAGEL, RODEO and RiPPMiner are dedicated to find ribosomally synthesized and post-translationally modified peptides (RIPPs). Then, implementing a further step, ARTs prioritizes previously detected BGCs (with antiSMASH) and identifies drug targets from these data.

You can also try to link diverse -omics data with genome predictions. SeMa-Trap allows the use RNA-Seq data to find co-expression patterns between certain genes and BGCs. Similarly, if you need to combine metabolomic/proteomic data with putative BGCs-products, you can use Pep2Path, NRPquest or RiPPquest, amongst others. 

There are also some tools and workflows that are dedicated to finding new biosynthetic systems (new types of BGCs or biosynthetic genes). Among them, EvoMining arose as a promising tool to detect biosynthetic enzymes that may have evolved from developing core functions ('central' or 'primary' metabolism) to carry on specialized functions (secondary metabolism). Likewise ClusterFinder enables the prediction of uncharacterized BGCs in genomes.

Also, to prioritize genomes or species, autoMLST allows not only to find phylogenetically closed strains/species from your input genome, but also to explore the biosynthetic potential of those relatives. 

FIXME


## Carpentries Philosophy
A good lesson should be as complete and clear that becomes easy to teach by any instructor. 
Carpentries lessons are developed for the community, and now you are part of us. 
This lesson is being developed and we are sure that you can colaborate and help us improve it.

{% include links.md %}


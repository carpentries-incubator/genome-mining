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

We have seen how to conduct a genome mining project with some particular characteristics. However, each research project may need some deviations to these workflows. You may need to make use of RNA-Seq data to search just for some specific domains instead of complete BGCs or to combine metabolomics or proteomics with genomic data. Here we will provide a list of resources that are also useful for genome mining projects.

First, since BGCs usually encompass genes with high levels of repeat regions (mainly NRPSs and PKSs), genome assemblers are not always capable of reconstructing BGCs and sometimes divide them into two contigs. To overcome this difficulty, you can use biosyntheticSPADes to assemble your reads into complete BGCs. This algorithm is implemented within the
[SPAdes](https://github.com/ablab/spades) tool.

Depending on your interests, you can use some alternative program to search for BGCs in your genomes. The [Secondary Metabolite Bioinformatics Portal](https://www.secondarymetabolites.org/) lists and introduces many diverse bioinformatic tools that pursue this goal. For example, [CLUSEAN](https://bitbucket.org/tilmweber/clusean/src/master/) and [NaPDoS](https://npdomainseeker.sdsc.edu/) allow to detect PKS and NRPS domains, while [BAGEL](http://bagel4.molgenrug.nl/), [RODEO](http://www.ripp.rodeo/) and [RiPPMiner](http://www.nii.ac.in/~priyesh/lantipepDB/new_predictions/index.php) are dedicated to find ribosomally synthesized and post-translationally modified peptides (RIPPs). Then, implementing a further step, [ARTS](https://arts.ziemertlab.com) prioritizes previously detected BGCs (with antiSMASH) and identifies drug targets from these data.

You can also try to link diverse -omics data with genome predictions. [SeMa-Trap](https://sema-trap.ziemertlab.com/) allows the use RNA-Seq data to find co-expression patterns between certain genes and BGCs. Similarly, if you need to combine metabolomic/proteomic data with putative BGCs-products, you can use [Pep2Path](http://pep2path.sourceforge.net), [MetaMiner](https://github.com/mohimanilab/MetaMiner) or [GNPS](https://gnps.ucsd.edu/ProteoSAFe/static/gnps-splash.jsp?redirect=auth), amongst others. 

There are also some tools and workflows that are dedicated to finding new biosynthetic systems (new types of BGCs or biosynthetic genes). Among them, as it was explained in previous lessons, [EvoMining](https://github.com/nselem/evomining) arose as a promising tool to detect biosynthetic enzymes that may have evolved from developing core functions ('central' or 'primary' metabolism) to carry on specialized functions (secondary metabolism). Likewise, [ClusterFinder](https://github.com/petercim/ClusterFinder) enables the prediction of uncharacterized BGCs in genomes through different algorithms.

Finally, to prioritize genomes or species, [autoMLST](https://automlst.ziemertlab.com/) allows you not only to find phylogenetically closed strains/species from your input genome but also to explore the biosynthetic potential of those relatives. 

## Visualize annotated genomes  
[CGView](https://github.com/paulstothard/cgview)

## Carpentries Philosophy
A good lesson should be as complete and transparent as easy to teach by any instructor. 
Carpentries lessons are developed for the community; now, you are part of us. 
This lesson is being developed, and we are sure that you can collaborate and help us improve it.

{% include links.md %}


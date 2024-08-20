---
title: "Metabolomics workshop"
teaching: 15 min
exercises: 75 min
questions:
- "How can I evaluate the similarity between MS spectra?"
objectives:
- "Understand how GNPS molecular networks work."
- "Use raw mzML metabolomic data for annotation."
- "Visualize and explore molecular networks"
keypoints:
- "Data is generated using Liquid Chromatography coupled to a tandem mass spectrometer (LC-MS/MS or MS2)."
- "Dereplication is the process of identifying previously known compounds."
- "Molecular networking is a computational method that organizes MS2 data based on spectral similarity, allowing us to infer relationships between chemical structures"
- "Feature-Based Molecular Networking (FBMN) enhances classical molecular networking by integrating relative quantitative data, enabling more robust metabolomics statistical analysis."
---

## Introduction

In the previous sections, we explored the biosynthetic potential of various strains by analyzing the BGCs within their genomes. We utilized BiG-SCAPE to create BGC networks, which compare all the BGCs detected by antiSMASH to determine their relatedness. 
Similarly, using metabolomics we can investigate the metabolites produced by selected strains in the laboratory. While crude extracts can be made to analyze the metabolites of specific strains, it is also possible to study the metabolites present in complex samples, such as soil, marine environments, host organisms, or stool samples.
There are two approaches to annotating metabolomics data. The first comprises using the information obtained by LC-MS, comparing the exact mass and UV spectra of each detected metabolite through natural product databases.
The introduction of the global natural products social molecular networking [GNPS](https://gnps.ucsd.edu/ProteoSAFe/static/gnps-splash.jsp) platform for molecular networking (M. Wang et al., 2016), significantly influenced dereplication techniques. Molecular networking groups metabolites into molecular families (MFs), thereby improving the annotation process of unknown metabolites.

<a href="../fig/Molecular-network.png">
  <img src="../fig/Molecular-network.png" alt="GNPS output can be directly visualized in the GNPS webpage, or using other visualization tools such as [Cytoscape](https://cytoscape.org/) " />
</a>

## Creating a GNPS account

Before starting this tutorial, it will be useful to have a GNPS account. For that go to the [GNPS](https://gnps.ucsd.edu/ProteoSAFe/static/gnps-splash.jsp) webpage and select Create a new account.
<a href="../fig/create_GNPSaccount.jpg">
  <img src="../fig/create_GNPSaccount.jpg" alt="Create an account in GNPS" />
</a>

Then fill in the following information: 
  -Username	
  -Name	
  -Organization	
  -Email	
  -Password
Wait for a confirmation email, and you now have a GNPS account.

## Download the metabolomics dataset






In the future it will include:
https://www.tfleao.com/general-8, 
[Paired omics](https://pairedomicsdata.bioinformatics.nl/)
[GNPS](https://gnps.ucsd.edu/ProteoSAFe/static/gnps-splash.jsp)

{% include links.md %}

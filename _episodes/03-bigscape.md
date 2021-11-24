---
title: "BigScape"
teaching: 0
exercises: 0
questions:
- "Key question (FIXME)"
objectives:
- "First learning objective. (FIXME)"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---
FIXME

# BiG-SCAPE

## Introduction

We learnt how to study the BGCs encoded by each of the genomes of our analyses. In case you are interested in the study of a certain BGC or a certain strain, this may be enough. However, sometimes the researcher aim to compare the biosynthetic potential of tens or hundreds of genomes. To perform this kind of analysis, we will use BiG-SCAPE, a workflow that will compare all the BGCs detected by antiSMASH to find their relateness. BiG-SCAPE will search for Pfam domains (Mistry et al., 2021) in the protein sequences of each BGC. Then, the Pfam domains will be linearized compared, creating different similarity networks and scoring the similarity of each pair of clusters. Based on this, the diverse BGCs will be classified on Gene Cluster Families (GCFs) to facilitate their study. A single GCF is supposed to encompass BGCs that produce chemically related metabolites (molecular families).

Let's see how this analysis can be done:

## Preparing the input

First, we need to create a folder with all the BGC files annotated by antiSMASH. 

`mkdir BGCs_antiSMASH`

In each of the antiSMASH output folders, we will find a single .gbk file for each BGC that include "region" within its filename. Thus, we will copy all those files to the new folder.

`cp */*.region*.gbk BGCs_antiSMASH/`

## Executing BiG-SCAPE




### References
Mistry, J., Chuguransky, S., Williams, L., Qureshi, M., Salazar, G. A., Sonnhammer, E. L., ... & Bateman, A. (2021). Pfam: The protein families database in 2021. Nucleic Acids Research, 49(D1), D412-D419.
{% include links.md %}

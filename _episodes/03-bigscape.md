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

We learnt how to study the BGCs encoded by each of the genomes of our analyses. In case you are interested in the study of a certain BGC or a certain strain, this may be enough. However, sometimes the researcher aim to compare the biosynthetic potential of tens or hundreds of genomes. To perform this kind of analysis, we will use BiG-SCAPE, a workflow that will compare all the BGCs detected by antiSMASH and it will create similarity networks among them. Also, the diverse BGCs will be classified on Gene Cluster Families (GCFs) to facilitate their study. Let's see how this analysis can be done:

## Preparing the input

First, we need to create a folder with all the BGC files annotated by antiSMASH. 

`mkdir BGCs_antiSMASH`

In each of the antiSMASH output folders, we will find a single .gbk file for each BGC that include "region" within its filename. Thus, we will copy all those files to the new folder.

`cp */*.region*.gbk BGCs_antiSMASH/`

## Executing BiG-SCAPE


{% include links.md %}

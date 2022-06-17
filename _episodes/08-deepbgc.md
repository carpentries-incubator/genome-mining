---
title: "BGC Prediction Through Machine Learning"
teaching: 0
exercises: 0
questions:
- ""
- ""
- ""
objectives:
- ""
- ""
- ""
keypoints:
- "First key point. Brief Answer to questions. (deepbgc, deep learning, natural language processing, genome mining, secondary metabolism, bacteria, bioactive coumpounds)"
---

# DeepBGC

## Introduction

As studied in previous sections, several BGC prediction algorithms have been developed. However their ability to identify novel BGC classes could be improved. DeepBGC(Hannigan, G. D., et al. 2019) represents a [Natural Language Processing](https://www.techtarget.com/searchenterpriseai/definition/natural-language-processing-NLP) and Deep Learning strategy for BGC prediction with reduced false positive rates and improved ability to identify novel BGC classes. DeepBGC helps uncover BGC not predicted by non-deep learning strategies. 

DeepBGC trains a model from a set of reference genomes whose protein family domains are identified by HMMER and the Pfam database. The genomes are embedded in a 100-dimensional vector space with NLP algorithm Pfam2vec. 

Para poner codigo
~~~
$ codigo
~~~
{: .bash}

Using output
~~~
$ output
~~~
{: .output}


### References

Hannigan, G. D., et al. "A deep learning genome-mining strategy for biosynthetic gene cluster prediction", Nucleic Acid Research (2019)

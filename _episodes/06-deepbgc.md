---
title: "DeepBGC"
teaching: 20
exercises: 30
questions:
- "What is DeepBGC?"
- "Which kind of analysis antiSMASH can perform?"
- "Which files extension accepts antiSMASH?"
objectives:
- "Understand how antiSMASH applications."
- "Understand the importance of metadata and potential metadata standards."
- "Explore common formatting challenges in spreadsheet data."
keypoints:
- "First key point. Brief Answer to questions. (deepbgc, deep learning, natural language processing, genome mining, secondary metabolism, bacteria, bioactive coumpounds)"
---

# DeepBGC

## Introduction

As studied in previous sections, several BGC prediction algorithms have been developed. However their ability to identify novel BGC classes could be improved. DeepBGC(Hannigan, G. D., et al. 2019) represents a [Natural Language Processing](https://www.techtarget.com/searchenterpriseai/definition/natural-language-processing-NLP) and deep learning strategy for BGC prediction with reduced false positive rates and improved ability to identify novel BGC classes. We will use DeepBGC to uncover BGC not predicted by non-deep learning strategies. Annotated genomes whose domains are identified using HMMER and the Pfam database are embedded in a 100-dimensional vector space with NLP algorithm Pfam2vec. 

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

---
title: "Antismash"
teaching: 20
exercises: 30
questions:
- "What is antiSMASH?"
- "Which kind of analysis antiSMASH can perform?"
- "Which files extension accepts antiSMASH?"
objectives:
- "Understand how antiSMASH applications."
- "Understand the importance of metadata and potential metadata standards."
- "Explore common formatting challenges in spreadsheet data."
keypoints:
- "First key point. Brief Answer to questions. (antismash, genome mining, secondary metabolism, bacteria, bioactive coumpounds)"
---

# antiSMASH

"The secondary metabolism of bacteria and fungi constitutes a rich source of bioactive compounds of potential pharmaceutical value, comprising biosynthetic pathways of many chemicals that have been and are being utilized as e.g. antibiotics, cholesterol-lowering drugs or antitumor drugs. Interestingly, the genes encoding the biosynthetic pathway responsible for the production of such a secondary metabolite are very often spatially clustered together at a certain position on the chromosome; such a compendium of genes is referred to as a 'secondary metabolite biosynthesis gene cluster'. This genetic architecture has opened up the possibility for straightforward detection of secondary metabolite biosynthesis pathways by locating their gene clusters. In recent years, the costs of sequencing bacterial and fungi has dropped dramatically, and many genome sequences have become available. Based on profile hidden Markov models of genes that are specific for certain types of gene clusters, antiSMASH is able to accurately identify the gene clusters encoding secondary metabolites of all known broad chemical classes. antiSMASH not only detects the gene clusters, but also offers detailed sequence analysis."

# Profile Hidden Markov Models

## Definition

Profile Hidden Markov's models are computational algorithms that predict protein structure identifying significant protein similarities letting a homologs detection. These probabilistic models:

- Encapsulate evolutionary changes that occurred in a set of related sequences.

Some applications are on gene finding, construction of genetic linkage maps (Turn multiple sequence alignment into a position-specific scoring system suitable for searching databases for remotely homologous sequences), and construction of physical maps. The most highlighted advantage is that this model has better gap dealing methods in proteins families.

![profile Markov Hidden Models](G:/Documentos/Axel/ITESM/Academic/DCC/1st_Semester/Pre-proposal/image.jpeg)

~
pwd
~
{: .source}

FIXME

{% include links.md %}
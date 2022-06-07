---
source: md
title: "BiGSlice / BiGFAM"
teaching: --
exercises: --
questions:
- "?"
- "?"
objectives:
- "Understand why we want to run `BiGSLICE` and `BiGFAM` "
- "Learn what input do we need to run `BiGSLICE` and `BiGFAM`"
- "Run an example with our _Streptococcus_ data on both softwares"
- "Understand the obtained results"
keypoints:
- ""  
- ""
- ""
---

> ## Ejercicio `.challenge`
> As we have seen the structure of the input folder for BiGSLICE is quite difficult to get. Imagine "Sekiro" wants to copy the directory structure to use it for future BigSlice inputs.
> Consider the following directory structure:
> ```
>    └── input_folder/                    
>        ├── datasets.tsv           
>        ├── dataset_1/
>        |   ├── genome_1A/
>        |   |   ├── genome_1A.region001.gbk
>        |   |   └── genome_1A.region002.gbk
>        |   ├── genome_1B/
>        |   |   ├── genome_1B.region001.gbk
>        |   |   └── genome_1B.region002.gbk
>        ├── dataset_2/
>        |   ├── genome_2A/
>        |   |   ├── genome_2A.region001.gbk
>        |   |   └── genome_2A.region002.gbk
>        |   ├── genome_2B/
>        |   |   ├── genome_2B.region001.gbk
>        |   |   └── genome_2B.region002.gbk
>        └── taxonomy/
>            ├── taxonomy_dataset_1.tsv
>            └── taxonomy_dataset_2.tsv                     
> ```
> Which would be the commands to copy the directory structure without the files (just the folders)? <br>
> a)
> ```
> cp -r input_folder input_folder_copy
> cd input_foder_copy
> rm -r
> ```
> b)
> ```
> mv -r input_folder input_folder_copy
> rm input_folder_copy/dataset_1/genome_1A/* input_folder_copy/dataset_1/genome_1B/*
> rm input_folder_copy/dataset_2/genome_2A/* input_folder_copy/dataset_2/genome_2B/*
> rm input_folder_copy/taxonomy/*
> ```
> c)
> ```
> cp -r input_folder input_folder_copy
> rm input_folder_copy/dataset_1/genome_1A/* input_folder_copy/dataset_1/genome_1B/*
> rm input_folder_copy/dataset_2/genome_2A/* input_folder_copy/dataset_2/genome_2B/*
> rm input_folder_copy/taxonomy/*
> ```
> d)
> ```
> cp -r input_folder input_folder_copy
> rm input_folder_copy/dataset_1/genome_1A/* /genome_1B/*
> rm input_folder_copy/dataset_2/genome_2A/* /genome_2B/*
> rm input_folder_copy/taxonomy/*
> ```
> > ## Solution
> > c)
> > ```
> > cp -r input_folder input_folder_copy
> > rm input_folder_copy/dataset_1/genome_1A/* input_folder_copy/dataset_1/genome_1B/*
> > rm input_folder_copy/dataset_2/genome_2A/* input_folder_copy/dataset_2/genome_2B/*
> > rm input_folder_copy/taxonomy/*
> > ```
> {: .solution}
{: .challenge}

> ## Exercise 2. `.challenge`  
> Fill in the blank spaces to complete the command that would get the organism information from the .gbk file. 
> 
> <p style="text-align: center;"> grep ___________ -m1 ____________ .gbk </p>
<!-- >  <p style="text-align: center;"> -------------------------------------------WORDS---------------------------------------------- </p> -->
>  <p style="text-align: center;"> -B 3 &nbsp; &nbsp; &nbsp; -A 3 &nbsp; &nbsp; &nbsp; -a  &nbsp; &nbsp; &nbsp; 'Streptococcus' &nbsp; &nbsp; &nbsp; 'ORGANISM' &nbsp; &nbsp; &nbsp; 'gbk'</p>
>  
> 
> > ## Solution
> {: .solution}
{: .challenge}


{% include links.md %}

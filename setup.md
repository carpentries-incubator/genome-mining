---
layout: page
title: Setup
---

# Oveview

This workshop is designed to be run on pre-imaged Amazon Web Services (AWS)
instances. With the exception of a spreadsheet program, all of the command line software and data used in the workshop are hosted on an Amazon 
Machine Image (AMI). Please follow the instructions below to prepare your computer for the workshop:



## Required software

Description

> ## Windows

> ## MacOS X

> ## Linux
>  - The default shell is usually Bash and there is usually no need to install anything. To see if your default shell is Bash type echo $SHELL in a terminal and press the Enter key. If the message printed does not end with '/bash' then your default is something else and you can run Bash by typing bash.
{: .solution}


## Option A: Using the lessons with Amazon Web Services (AWS)

If you are signed up to take a Genome Mining Data Carpentry Workshop, you do *not* need to worry about setting up an AMI instance. The Carpentries
staff will create an instance for you and this will be provided to you at no cost. This is true for both self-organized and centrally-organized workshops. Your Instructor will provide instructions for connecting to the AMI instance at the workshop.

If you would like to work through these lessons independently, outside of a workshop, you will need to start your own AMI instance. 
Follow these [instructions on creating an Amazon instance](https://carpentries-incubator.github.io/metagenomics-workshop/AMI-setup/index.html). Use the AMI `ami-0e7fb76a881ab5e09` (Metagenomics - 18 March (The Carpentries Incubator)) listed on the Community AMIs page. Please note that you must set your location as `N. Virginia` in order to access this community AMI. You can change your location in the upper right corner of the main AWS menu bar. The cost of using this AMI for a few days, with the t2.medium instance type is very low (about USD $1.50 per user, per day). Data Carpentry has *no* control over AWS pricing structure and provides this cost estimate with no guarantees. Please read AWS documentation on pricing for up-to-date information. 

If you're an Instructor or Maintainer or want to contribute to these lessons, please get in touch with us [team@carpentries.org](mailto:team@carpentries.org) and we will start instances for you. 

After the basic software of the genomic instace is setup you need to add the metagenomics environment. 
Here is a link to [specifications file](https://github.com/AxelRamosGarcia/Genome-Mining/blob/gh-pages/files/GenomeMining.yml)  with the exact versions of each tool in this environment. You can use the spec file as follows:
> ~~~
> $ conda create --name myenv --file spec-file.txt
> ~~~
>{: .bash}

This environment can be modified by adding or deleting tools in a file `metagenomics.yml`, 
original metagenomics.yml file had the following content:  
~~~
$ cat GenomeMining.yml
~~~
{: .bash}
~~~
name: GenomeMining                                                                
dependencies:                                      
  - antismash=6.0.0
  - deepbgc=0.1.29             
  - BiG-SLiCE=1.1.0
~~~
{: .output}

Then you can create your own metagenomics conda environment using the metagenomics.yml file.  
> ~~~
> $ conda env create -f GenomeMining.yml
> ~~~
>{: .bash}

More information about how to use environments and spec file is available at [conda documentation](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)

### Evomining conda   
  
`git clone https://github.com/miguel-mx/evomining-conda`       
`cd evomining-conda`     
`conda env create -f evomining.yml --prefix="/opt/anaconda3/envs/evomining-conda"`     

### Data

The data used in this workshop are available on Zenodo. Because this workshop works with real data, be aware that file sizes for the data are large. Please read the Zenodo page linked below for information about the data and access to the data files. 

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.6617709.svg)](https://doi.org/10.5281/zenodo.6617709)
{% include links.md %}

---
title: "Genome Mining Databases"
teaching: 15
exercises: 10
questions:
- "Where can I find experimentally validated BGCs?"
- "Where is information about all predicted BGCs?"
objectives:
- "Use MIBiG database as a source of experimentally tested BGC."
- "Explore antiSMASH database to learn about the distribution of predicted BGC."
keypoints:
- "MIBiG provides BGCs that have been experimentally tested"
- "antiSMASH database comprises predicted BGCs of each organism"
---
## MIBiG Database
The Minimum Information about a Biosynthetic Gene cluster 
[MIBiG](https://mibig.secondarymetabolites.org/repository) 
is a database that facilitates consistent and systematic deposition 
and retrieval of data on biosynthetic gene clusters. MIBiG provides 
a robust community standard for annotations and metadata on 
biosynthetic gene clusters and their molecular products. It will 
empower next-generation research on the biosynthesis, chemistry 
and ecology of broad classes of societally relevant bioactive 
secondary metabolites, guided by robust experimental evidence 
and rich metadata components.

### Browsing and Querying in the MIBiG database

Select "Search" on the upper right corner of the menu bar


<a href="{{ page.root }}/fig/MIBiG_search.png">
  <img src="{{ page.root }}/fig/MIBiG_search.png" alt="MIBiG website homepage highlighting the search tool" />
</a>

For simple queries, such as _Streptococcus agalactiae_ or searching for a specific strain you can use the "Simple search"  function.

<a href="{{ page.root }}/fig/MIBiG_query.png">
  <img src="{{ page.root }}/fig/MIBiG_query.png" alt="MIBiG website query page" />
</a>

For complex queries, the database also provides a sophisticated query builder that allows querying on all antiSMASH annotations. To enable this function, click on "Build a query"

### Results

<a href="{{ page.root }}/fig/MIBiG_results.png">
  <img src="{{ page.root }}/fig/MIBiG_results.png" alt="MIBiG website displaying the results from the simple search Streptococcus" />
</a>

> ## Exercise 1: 
> Enter to [MIBiG](https://mibig.secondarymetabolites.org/) and search BGCs from *Streptococcus*. Search the BGCs that produce the products Thermophilin 1277 and Streptolysin S. Based on the table on MIBiG, which of these organisms has the most complete annotation?
> 
> > ## Solution
> > _Streptococcus thermophilus_ produce Thermophilin 1277 while _Streptococcus pyogenes_ M1 GAS produces Streptolysin S.
> > According to MIBiG metadata Streptolysin S BGC is complete while Thermophilin 1277 is not.
> > So Streptolysin S BGC is better annotated. 
> {: .solution}
{: .challenge}



## antiSMASH database
The [antiSMASH database](https://antismash-db.secondarymetabolites.org/) 
provides an easy to use, up-to-date collection of 
annotated BGC data. It allows to easily perform cross-genome 
analyses by offering complex queries on the datasets.

### Browsing and Querying in the antiSMASH database
Select "Browse" on the top menu bar, alternatively you can select "Query" in the center

<a href="{{ page.root }}/fig/antiSMASH_db.png">
  <img src="{{ page.root }}/fig/antiSMASH_db.png" alt="antiSMASH website homepage" />
</a>

For simple queries, such as "_Streptococcus_" or searching for a 
specific strain you can use the "Simple search" function.

<a href="{{ page.root }}/fig/antiSMASH_search.png">
  <img src="{{ page.root }}/fig/antiSMASH_search.png" alt="antiSMASH website query page" />
</a>

For complex queries, the database also provides a sophisticated query 
builder that allows querying on all antiSMASH annotations. To enable 
this function, click on "Build a query"

### Results

<a href="{{ page.root }}/fig/antiSMASH_query.png">
  <img src="{{ page.root }}/fig/antiSMASH_query.png" alt="antiSMASH website displaying the results from the simple search Streptococcus" />
</a>

Use antiSMASH database to analyse the BGC contained in 
the _Streptococcus_ genomes. We'll use Python to visualize
the data. First, import pandas, matplotlib.pyplot and seaborn
libraries.
  
~~~
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
~~~
{: .language-python}

Secondly, store in a dataframe variable the content of the
_Streptococcus_ predicted BGC downloaded from antiSMASH-db.  

~~~
data = pd.read_csv("https://raw.githubusercontent.com/AxelRamosGarcia/Genome-Mining/gh-pages/data/antismash_db.csv", sep="\t")
data
~~~
{: .language-python}

<a href="{{ page.root }}/fig/21-08-24-chapter9-table.png">
  <img src="{{ page.root }}/fig/21-08-24-chapter9-table.png" alt="a dataframe variable the content of the Streptococcus predicted BGC" width="800" />
</a>

Now, group the data by the variables Species and BGC type:  
~~~
occurences = data.groupby(["Species", "BGC type"]).size().reset_index(name="Occurrences")
~~~
{: .language-python}

And visualize the content of the ocurrences grouped by species column:  
~~~
occurences
~~~
{: .language-python}  

<a href="{{ page.root }}/fig/21-08-24-chapter9-occurences.png">
  <img src="{{ page.root }}/fig/21-08-24-chapter9-occurences.png" alt="the content of the ocurrences grouped by species column" width="500"/>
</a>

Let's see our first visualization of the BGC content on a heatmap.

~~~
pivot = occurences.pivot(index="BGC type", columns="Species", values="Occurrences")
plt.figure(figsize=(8, 10))
sns.heatmap(pivot, cmap="coolwarm")
plt.show()
~~~
{: .language-python}  

<a href="{{ page.root }}/fig/21-08-24-chapter9-heatmap.png">
  <img src="{{ page.root }}/fig/21-08-24-chapter9-heatmap.png" alt="visualization of the BGC content on a heatmap." width="800"/>
</a>


Now, let's restrict ourselves to _S. agalactiae_.

~~~
agalactiae = occurences[occurences["Species"] == "agalactiae"]
sns.scatterplot(agalactiae, x="BGC type", y="Occurrences")
plt.xticks(rotation="vertical")
plt.show()
~~~
{: .language-python}

<a href="{{ page.root }}/fig/21-08-24-chapter9.dotplot.png">
  <img src="{{ page.root }}/fig/21-08-24-chapter9.dotplot.png" alt="visualization of the BGC content of S. agalactiae. on a sctterplot" width="800"/>
</a>

Finally, let's restrict ourselves to BGC predicted less than 200 times.

~~~
filtered = occurences[occurences["Occurrences"] < 200]
plt.figure(figsize=(15, 5))
sns.scatterplot(filtered, x="BGC type", y="Occurrences")
plt.xticks(rotation="vertical")
plt.grid(axis="y")
plt.show()
~~~
{: .language-python}

<a href="{{ page.root }}/fig/21-08-24-chapter9.dotplot2.png">
  <img src="{{ page.root }}/fig/21-08-24-chapter9.dotplot2.png" alt="visualization of the BGC content on a scatterplot" width="800"/>
</a>

~~~
filtered_pivot = filtered.pivot(index="BGC type", columns="Species", values="Occurrences")
plt.figure(figsize=(8, 10))
sns.heatmap(filtered_pivot, cmap="coolwarm")
plt.show()
~~~
{: .language-python}

<a href="{{ page.root }}/fig/21-08-24-chapter9-pivot-filtered.png">
  <img src="{{ page.root }}/fig/21-08-24-chapter9-pivot-filtered.png" alt="filtered heatmap " width="800"/>
</a>


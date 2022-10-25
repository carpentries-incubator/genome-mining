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
- "MIBiG provides BGCs that have been experimentally tested."
- "antiSMASH database comprises predicted BGCs of each organism."
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

> ![Forking Repositories]({{ page.root }}/fig/MIBiG_search.png)

For simple queries, such as _Streptococcus agalactiae_ or searching for a specific strain you can use the "Simple search"  function.

> ![Forking Repositories]({{ page.root }}/fig/MIBiG_query.png)

For complex queries, the database also provides a sophisticated query builder that allows querying on all antiSMASH annotations. To enable this function, click on "Build a query"

### Results

> ![Forking Repositories]({{ page.root }}/fig/MIBiG_results.png)

> ## Exercise 1: 
> You are going to do an experiment, you have two organisms one is likely to produce *themophilin 1277* and the other one *streptolysin S*, based on the table, which of these organisms is more likely to produce their respective secondary metabolite?
> 
> > ## Solution
> > Todavía no hay
> {: .solution}
{: .challenge}



## antiSMASH database
The [antiSMASH database](https://antismash-db.secondarymetabolites.org/) 
provides researchers with an easy to use, up-to-date collection of 
annotated BGC data, which enable them to easily perform cross-genome 
analyses by offering complex queries on the datasets

### Browsing and Querying in the antiSMASH database
Select "Browse" on the top menu bar, alternatively you can select "Query" in the center

> ![Forking Repositories]({{ page.root }}/fig/antiSMASH_db.png)

For simple queries, such as "Streptococcus" or searching for a 
specific strain you can use the "Simple search" function.

> ![Forking Repositories]({{ page.root }}/fig/antiSMASH_search.png)

For complex queries, the database also provides a sophisticated query 
builder that allows querying on all antiSMASH annotations. To enable 
this function, click on "Build a query"

### Results

> ![Forking Repositories]({{ page.root }}/fig/antiSMASH_query.png)
Let's use antiSMASH database to know the BGC contained in 
the _Streptococcus_ genomes. We will use R to visualize the data.  
Firstly, ativate two libraries, `dplyr` for data manipulation 
and `ggplot2` for data visualization.      
  
~~~
library("dplyr")
library("ggplot2")
~~~
{: .language-r}

Secondly, store in a dataframe variable the content of the
_Streptococcus_ predicted BGC downloaded from antiSMASH-db.  

~~~
df <- read.csv(file = "gm_workshop/data/antismash_db.csv", stringsAsFactors = TRUE)
~~~
{: .language-r}

Now, group the data by the variables Species and BGC.type:  
~~~
Streptococcus_antismash_df<-df %>%  group_by(Species,BGC.type) %>%  summarize(occurrences = n()) 
~~~
{: .language-r}

And visualize the content of the Species column:  
~~~
Streptococcus_antismash_df$Species 
~~~
{: .language-r}  

Let's see our first visualization of the BGC content on a heatmap  .
~~~
Streptococcus_antismash_plot<-ggplot(Streptococcus_antismash_df, aes(x = Species, y = BGC.type, fill = occurrences)) + geom_tile() 
ggsave(filename = "gm_workshop/results/Streptococcus_antismash_plot.png", plot = Streptococcus_antismash_plot, width = 20, height = 10, dpi = 300, units = "cm")
~~~
{: .language-r}  

To improve legend legibility run the following command:
~~~
Streptococcus_antismash_plot<-ggplot(Streptococcus_antismash_df, aes(x = Species, y = BGC.type, fill = occurrences)) + geom_tile() 
+ theme(axis.text.x=element_text(angle = 90))#+ scale_fill_gradient(low = "white", high = "steelblue")
ggsave(filename = "gm_workshop/results/Streptococcus_antismash_plot.png", plot = Streptococcus_antismash_plot, width = 20, height = 10, dpi = 300, units = "cm")

~~~
{: .language-r}

Now, let's restrict ourselves to _S. agalactiae_  
~~~
df_agalactiae<-Streptococcus_antismash_df[(Streptococcus_antismash_df$Species=="agalactiae"),]             
agalactiae_plot<-ggplot(df_agalactiae, aes( x = BGC.type, y = occurrences)) + geom_point() + theme(axis.text.x=element_text(angle = 90))
ggsave(filename = "gm_workshop/results/agalactiae_plot.png", plot = agalactiae_plot, width = 20, height = 10, dpi = 300, units = "cm")
~~~
{: .language-r}

Finally, since _S. pneumonia_ lets restrict ourselves 
to BGC predicted less than 200 times.   
~~~
df2<-Streptococcus_antismash_df[!(Streptococcus_antismash_df$occurrences>200),]             
Streptococcus_smooth_plot<-ggplot(df2, aes(x = BGC.type, y = occurrences)) + geom_tile() + theme(axis.text.x=element_text(angle = 90))+ scale_fill_gradient(low = "white", high = "steelblue")
ggsave(filename = "gm_workshop/results/Streptococcus_smooth_plot.png", plot = Streptococcus_smooth_plot, width = 20, height = 10, dpi = 300, units = "cm")

Streptococcus_smooth_plot2<-ggplot(df2, aes(x = Species, y = BGC.type, fill = occurrences)) + geom_tile() + theme(axis.text.x=element_text(angle = 90))#+ scale_fill_gradient(low = "white", high = "steelblue")
ggsave(filename = "gm_workshop/results/Streptococcus_smooth_plot.png", plot = Streptococcus_smooth_plot, width = 20, height = 10, dpi = 300, units = "cm")
~~~
{: .language-r}

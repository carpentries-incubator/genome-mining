---
title: "antiSMASH database and MIBiG"
teaching: 15
exercises: 10
questions:
- "How can I validate my antiSMASH's outputs?"
- "Which kind of analysis antiSMASH can perform?"
- "Which files extension accepts antiSMASH?"
objectives:
- "Understand how antiSMASH applications."
- "Understand the importance of metadata and potential metadata standards."
- "Explore common formatting challenges in spreadsheet data."
keypoints:
- "antiSMASH predict BGCs that are antibiotic producers of each organism"
- "MIBiG show BGCs that have been tested with an experiment."
---
## MIBiG Database
The Minimum Information about a Biosynthetic Gene cluster (MIBiG) is a database that facilitates consistent and systematic deposition and retrieval of data on biosynthetic gene clusters. MIBiG provides a robust community standard for annotations and metadata on biosynthetic gene clusters and their molecular products. It will empower next-generation research on the biosynthesis, chemistry and ecology of broad classes of societally relevant bioactive secondary metabolites, guided by robust experimental evidence and rich metadata components.

### Browsing and Querying in the MIBiG database

Select "Search" on the upper right corner of the menu bar

> ![Forking Repositories]({{ page.root }}/fig/MIBiG_search.png)

For simple queries, such as "Streptococcus agalactiae" or searching for a specific strain you can use the "Simple search"  functionality.

> ![Forking Repositories]({{ page.root }}/fig/MIBiG_query.png)

For complex queries the database also provides a sophisticated query builder that allows querying on all antiSMASH annotations. To enable this function, click on "Build a query"

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
The antiSMASH database provides researchers with an easy to use, up-to-date collection of annotated BGC data, which enable them to easily perform cross-genome analyses by offering complex queries on the datasets

### Browsing and Querying in the antiSMASH database
Select "Browse" on the top menu bar either you can select "Query" in the center

> ![Forking Repositories]({{ page.root }}/fig/antiSMASH_db.png)

For simple queries, such as "Streptococcus" or searching for a specific strain you can use the "Simple search" functionality.

> ![Forking Repositories]({{ page.root }}/fig/antiSMASH_search.png)

For complex queries the database also provides a sophisticated query builder that allows querying on all antiSMASH annotations. To enable this function, click on "Build a query"

### Results

> ![Forking Repositories]({{ page.root }}/fig/antiSMASH_query.png)

~~~
library("dplyr")
library(ggplot2)

df <- read.csv(file = "gm_workshop/data/antismash_db.csv", stringsAsFactors = TRUE)

mm<-df %>%
  group_by(Species,BGC.type) %>%
  summarize(se_le = n())

#names(mm)[names(mm) == 'BGC.type'] <- 'BGC_type'
ggplot(mm, aes(x = Species, y = BGC.type, fill = se_le)) + geom_tile() + theme(axis.text.x=element_text(angle = 90))#+ scale_fill_gradient(low = "white", high = "steelblue")

df2<-mm[(mm$Species=="agalactiae"),]             
ggplot(df2, aes( x = BGC.type, y = se_le)) + geom_point() + theme(axis.text.x=element_text(angle = 90))

df3<-mm[!(mm$se_le>200),]             


ggplot(df3, aes(x = BGC.type, y = se_le)) + geom_tile() + theme(axis.text.x=element_text(angle = 90))+ scale_fill_gradient(low = "white", high = "steelblue")

ggplot(df3, aes(x = Species, y = BGC.type, fill = se_le)) + geom_tile() + theme(axis.text.x=element_text(angle = 90))#+ scale_fill_gradient(low = "white", high = "steelblue")
~~~
{: .r-language}


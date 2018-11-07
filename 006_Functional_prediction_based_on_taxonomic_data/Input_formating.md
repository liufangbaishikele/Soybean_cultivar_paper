## Prepare dataset for Tax4Fun analysis 

----

Basically, there are mainly two steps to follow to format the dataset 


1. Combine genus level count table & taxonomy table

* Genus level count table and taxonomy table generation in mothur

```
sub.sample(list=cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.list,count=cultivar.trim.contigs.good.unique.good.filter.unique.precluster.denovo.vsearch.pick.pick.count_table,size=19023,persample=TRUE,label=1)
You have selected a size that is larger than blankH11 number of sequences, removing blankH11.
You have selected a size that is larger than blankH5 number of sequences, removing blankH5.
Sampling 19023 from each group.
1

Output File Names:
cultivar.trim.contigs.good.unique.good.filter.unique.precluster.denovo.vsearch.pick.pick.subsample.count_table
cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.subsample.list

remove.rare(list=cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.subsample.list,count=cultivar.trim.contigs.good.unique.good.filter.unique.precluster.denovo.vsearch.pick.pick.subsample.count_table,nseqs=50,label=1)

Output File Names:
cultivar.trim.contigs.good.unique.good.filter.unique.precluster.denovo.vsearch.pick.pick.subsample.pick.count_table
cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.subsample.1.pick.list


make.shared(list=cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.subsample.1.pick.list,count=cultivar.trim.contigs.good.unique.good.filter.unique.precluster.denovo.vsearch.pick.pick.subsample.pick.count_table,label=1)
1

Output File Names:
cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.subsample.1.pick.shared


classify.otu(list=cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.subsample.1.pick.list,count=cultivar.trim.contigs.good.unique.good.filter.unique.precluster.denovo.vsearch.pick.pick.subsample.pick.count_table,taxonomy=cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.taxonomy,label=1)
1       365

Output File Names:
cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.subsample.1.pick.1.cons.taxonomy
cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.subsample.1.pick.1.cons.tax.summary
```
* Transfer the generated ``.shared`` file and ``con.taxonomy`` file to local computer and do further edit in excel.
* Combine these two datasets together in as following:

```
sample1	sample2	sample3 ...sampleN 
count11	count12	count13	...count1n	Bacteria;Firmicutes;Bacilli;Bacillales;Bacillaceae_1;Bacillus;
.					.
.					.
.					.
countk1	countk2	countk3	...countkn	Bacteria;Planctomycetes;Planctomycetacia;Planctomycetales;Planctomycetaceae;Planctomyces;
```
* Save the aboved combined file as csv. However, this format still does not match with Tax4Fun input format (in my case, I used the SILVang output format)

* Transfer the combined csv file to our server and transfered to txt file

* Then convert txt file into csv (comman seperated) file and secure copy to local computer for Tax4Fun analysis in R.

* Detailed analysis in R could be found in ``Tax4Fun.Rmd``

* For the final heatmap results, we deleted metabolic pathways that not compatible with plant microbiome as the curated KEGG pathway were combined from human microbiome and plant microbiome as well as environmental microbiome.




  

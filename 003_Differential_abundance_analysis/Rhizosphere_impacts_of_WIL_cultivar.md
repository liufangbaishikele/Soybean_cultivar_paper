## This file will document the lefse analysis to infer selective bacterial genera enrichment or depletion in rhizosphere of specific cultivar.

1. Generate lefse input file in mothur based on OTU count table, taxonomy table as well as meta data.

```
sub.sample(shared=cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.shared,groups=Ag_B_1-Ag_B_10-Ag_B_11-Ag_B_12-Ag_B_2-Ag_B_3-Ag_B_4-Ag_B_5-Ag_B_6-Ag_B_7-Ag_B_8-Ag_B_9-Ag_WIL_1-Ag_WIL_10-Ag_WIL_2-Ag_WIL_3-Ag_WIL_4-Ag_WIL_5-Ag_WIL_6-Ag_WIL_7-Ag_WIL_8-Ag_Fresh_2-Ag_Fresh_3-Ag_Fresh_4-Ag_Fresh_5)
Sampling 20557 from each group.
1

Output File Names:
cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.1.subsample.shared


remove.rare(shared=cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.1.subsample.shared,nseqs=50)
1

Output File Names:
cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.1.subsample.1.pick.shared


make.lefse(shared=cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.1.subsample.1.pick.shared,constaxonomy=cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.cons.taxonomy,scale=totalgroup,design=Ag_soil_vs_WIL.design)
You did not provide a label, I will use the first label in your inputfile.

Output File Names:
cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.1.subsample.1.pick.1.lefse
```


2. LefSe analysis 

```
lefse-format_input.py cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.1.subsample.1.pick.1.lefse cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.1.subsample.1.pick.1.lefse_in  -c 1 -s -1 -u 2 -o 1000000

run_lefse.py cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.1.subsample.1.pick.1.lefse_in cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.1.subsample.1.pick.1.lefse_res_LDA2 -l 2 -b 200 -t Ag_soil_vs_WIL_Genus_LefSe_LDA2 -y 1

lefse-plot_res.py cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.1.subsample.1.pick.1.lefse_res_LDA2 cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.1.subsample.1.pick.1.lefse_res_LDA2.png --dpi 300 --title Ag_soil_vs_WIL_Genus_LefSe_LDA2.png
```


3. Extract bacterial genera that significantly enriched or depleted in soybean rhizopshere

```
grep 'Soil' cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.1.subsample.1.pick.1.lefse_res_LDA2 > Ag_WIL_depleted_list
grep 'Otu...' Ag_WIL_depleted_list | sort > Ag_WIL_depleted_genus
awk 'NR%2==0' Ag_WIL_depleted_genus > Ag_WIL_depleted_genus_update


grep 'Rhizosphere' cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.1.subsample.1.pick.1.lefse_res_LDA2 > Ag_WIL_enriched_list
grep 'Otu...' Ag_WIL_enriched_list | sort > Ag_WIL_enriched_genus
awk 'NR%2==0' Ag_WIL_enriched_genus > Ag_WIL_enriched_genus_update
``` 

4. These differentially selected genera will be converted to csv file, which will then be used to generate circular phylogenetic tree based on LDA (linear discriminant analysis) score.

Subsequent visualization were completed using GraPhlAn. 



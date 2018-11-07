### Commands within mothur

1. subset samples to include samples used for LefSe based on the comparison. Meanwhile, rarefy reads to minimum read depth at 19023.
e.g., between rhizosphere and soi microbiome

```
sub.sample(shared=cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.shared,size=19023,groups=Ag_B_10-Ag_B_11-Ag_B_12-Ag_B_1-Ag_B_2-Ag_B_3-Ag_B_4-Ag_B_5-Ag_B_6-Ag_B_7-Ag_B_8-Ag_B_9-Ag_CV1_10-Ag_CV1_1-Ag_CV1_2-Ag_CV1_3-Ag_CV1_4-Ag_CV1_5-Ag_CV1_6-Ag_CV1_7-Ag_CV1_8-Ag_CV1_9-Ag_CV2_1-Ag_CV2_2-Ag_CV2_3-Ag_CV2_4-Ag_CV2_5-Ag_CV2_6-Ag_CV2_7-Ag_CV2_8-Ag_CV3_1-Ag_CV3_2-Ag_CV3_3-Ag_CV3_4-Ag_CV3_5-Ag_CV3_6-Ag_CV3_7-Ag_CV3_8-Ag_CV3_9-Ag_CV4_1-Ag_CV4_2-Ag_CV4_3-Ag_CV4_4-Ag_CV4_5-Ag_CV4_6-Ag_CV4_7-Ag_CV4_8-Ag_CV4_9-Ag_CV5_1-Ag_CV5_2-Ag_CV5_3-Ag_CV5_4-Ag_CV5_5-Ag_CV5_6-Ag_CV5_7-Ag_CV6_1-Ag_CV6_2-Ag_CV6_3-Ag_CV6_4-Ag_CV6_5-Ag_CV6_6-Ag_CV6_7-Ag_CV6_8-Ag_Fresh_1-Ag_Fresh_2-Ag_Fresh_3-Ag_Fresh_4-Ag_Fresh_5)
```

2. Remove rare sequences, whose reads smaller than 50 across all samples.
```
remove.rare(shared=cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.1.subsample.shared,nseqs=50)
```

3. Use make.lefse command in mothur to create lefse file, which include both count, taxonomy and treatment information.

```
make.lefse(shared=cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.1.subsample.1.pick.shared,constaxonomy=cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.cons.taxonomy,design=Ag_compartment.design,scale=totalgroup)
```

Output file: cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.1.subsample.1.pick.1.lefse

4. Once lefse file were prepared in mothur. Pipe it to Lefse for further analysis.

About detailed parameter setup, just type in command -h, e.g., ``lefse-format_input.py -h``
```
lefse-format_input.py cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.1.subsample.1.pick.1.lefse cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.1.subsample.1.pick.1.lefse_in  -c 1 -s -1 -u 2 -o 1000000

run_lefse.py cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.1.subsample.1.pick.1.lefse_in cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.1.subsample.1.pick.1.lefse_res_LDA4 -l 4 -b 200 -t Ag_compartment_OTU_lefse_LDA4 -y 1

lefse-plot_res.py cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.1.subsample.1.pick.1.lefse_res_LDA4 cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.1.subsample.1.pick.1.lefse_res_LDA4.png --dpi 300 --title Ag_compartment_LefSE_LDA4.png
```

5. Further edits on the LDA output in order to plot more elegant images.

  *First grep all significantly different taxa to temp file by ``grep 'Rhizosphere' file> temp`` & ``grep 'Soil' file >> temp``
  *Remove all Otu... rows due to information duplication
  *And removed other duplicated information. e.g., Bacteria_unclassifed at differnt taxa level with same LDA value

6. Update the Lefse output images

```
lefse-plot_res.py cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.1.subsample.1.pick.1.lefse.res_LDA4_edit cultivar.trim.contigs.good.unique.good.filter.unique.precluster.pick.pds.wang.pick.tx.1.1.subsample.1.pick.1.lefse.res_LDA4_edit.png --title "Agriculture Soil vs Rhizosphere Microbiome" --dpi 300 --feature_font_size 8 --title_font_size 16 --class_legend_font_size 12 --width 7 --height 4 --left_space 0.1 --right_space 0.1
```



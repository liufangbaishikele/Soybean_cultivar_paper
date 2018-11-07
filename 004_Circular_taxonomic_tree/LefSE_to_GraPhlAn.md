### From LefSe results to GraPhlAn

----
To provide more informative visualization of the differentially enriched/depleted bacterial genera across treatments, circular phylogenetic tree were created by GraPhlAn based on LefSE output data.


1. The output LDA2 file were modified to exclude non significant genus with LDA score smaller than 

2. Then the LDA list were subset to two dataset that include enriched and depleted genus as well as LDA score values.

3. Significantly enriched or depleted genus in each treatment were merged to use as input for graphlan software. Detailed dataset manipulation could be found from ``003_Differential_abundance_analysis`` R markdown file.

4. Generate phylogenetic tree file as well as annotation file using R commands. Detailed code please find in 003_Differential_abundance_analysis/Lefse_based_genus_enrichment_in_Rhi.Rmd.

5. Plot phylogenetic tree based on step4 generated taxonomy and annotation information. Detailed tree file and annotation file could be find in zipped file.

```
python graphlan_annotate.py LDA_tree LDA_annot_09_up_tree --annot LDA_annot_09_up
python graphlan.py LDA_annot_09_up_tree LDA_annot_09_up_tree2.png --dpi 220 --size 19 --pad 2 
```

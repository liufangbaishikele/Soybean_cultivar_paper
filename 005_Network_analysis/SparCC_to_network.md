### SparCC were installed on our server using anaconda

*The OTU table for SparCC calculation were prepared as documented in the ``Cultivar_SparCC_3rd_analysis.Rmd``*

###SparCC analysis process in our server.
1. Calculate SparCC correlation between OTUs

*The OTU table for SparCC calculation were prepared as documented in the Rmd file*

/staton/software/Anaconda2-2.5.0/bin/python2 /staton/projects/soybean_rhizosphere/2016_cultivar/03_SparCC/SparCC_code/MakeBootstraps.py  Ag_soil/Ag_soil_OTU_SparCC.txt -n 200 --template=Ag_soil_OTU_otu_count_permutation#.txt --path=Ag_soil/pvals/bootstrap_simulation/
2. Using bootstraping to generate 200 random OTU count table based on the original one. This is preparing datasets for downward significant test on each correlation.

for ((i=0;i<=199;i++))
do
  echo $i
  /staton/software/Anaconda2-2.5.0/bin/python2 /staton/projects/soybean_rhizosphere/2016_cultivar/03_SparCC/SparCC_code/SparCC.py Ag_soil/pvals/bootstrap_simulation/Ag_soil_OTU_otu_count_permutation"$i".txt -i 20 --cor_file=Ag_soil/pvals/bootstrap_corr/Ag_soil_OTU_bootstrap_permutation"$i"_corr.txt -a SparCC
done

3. Calculate the p value for each correlation using ``PseudoPvals.py`` command.

/staton/software/Anaconda2-2.5.0/bin/python2 /staton/projects/soybean_rhizosphere/2016_cultivar/03_SparCC/SparCC_code/PseudoPvals.py Ag_soil/basis_corr/Ag_soil_OTU_cor_sparcc.txt Ag_soil/pvals/bootstrap_corr/Ag_soil_OTU_bootstrap_permutation#_corr.txt 200 -o Ag_soil/pvals/Ag_soil_OTU_two_sided_pvalue.txt -t two_sided

4. Repeat the calculation for each treatment including: Ag_Soil, Ag_WIL, Ag_DRT, Ag_CNR, Ag_NNW, Ag_SOJ, Ag_W82, For_Soil, For_WIL, For_DRT, For_CNR, For_NNW, For_SOJ, For_W82.

5. Then convert the output SparCC correlation table as well as the two_side p value matrix from txt to csv. Secure copy to local computer and continue network analysis and visualization in R using Igraph packages. Detailed commands were provided in ``Cultivar_SparCC_3rd_analysis.Rmd``  



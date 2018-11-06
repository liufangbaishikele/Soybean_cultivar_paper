# Soybean_cultivar_paper
This repository were modified from soybean_rhizosphere_microbiome repository to make it into a systemic one


**Paper title**: Soil indigenous microbiome and plant genotypes cooperatively modify soybean rhizosphere microbiome assembly
  
> Date 11-04-2018 . 

> Author Fang Liu . 

This is the documentation about the whole project, including experiment design, sequencing plan and data analysis.
------

**Experiment design**

 * The experiment were set up inside of the greenhouse as a controled system. To investigate the impacts of plant genetic traits and soil background, we designed two factorial experiment.
 * To infer plant genetic traits impacts, we selected five soybean cultivars with different physiologies, including Williams (WIL), Non-nodulating mutant of William (NNW), Williams 82 (W82), Cyst nematode resistant (CNR), Drought tolerant (DRT) as well as a progenty line, Glycine soja (SOJ). Similarly, two soil type, i.e., agriculture (Ag) and forest (For) soil were included as the soil type factor.

 * At flowering stage, rhizosphere soil and bulk soil (treated the same inside of greenhouse but without soybean growing) were harvested. DNA were extracted using PowerSoil kit and subjected for 16S rRNA gene sequencing targeted V3-4 region.

**Sequencing process**

 * The 16S rRNA gene sequencing data were processed in Mothur to generate OTU count and taxonomy information following main the Miseq SOP pipeline.
 * For subsequent analysis purpose, subset, remove rare, make.lefse, rarefaction, etc commands were used for different purpose.

** Further data analysis using R, shell command as well as python.

 * For community analysis, including microbial composition, similarity as well as variantion analysis were done mainly using Phyloseq package of R.

 * For differential abundance analysis, LefSE were used at different LDA level.

 * GraPhlAn were used for comprehensive visualization of bacterial genera enrichment and delpletion across all treatment.

 * To infer microbe-microbe interaction pattern between treatment, SparCC was used to generate correlation matrix as well as significance. Igraph were used to generate network and calculate network topological characteristics.

 * For microbiome function investigation, Tax4Fun were used to predict the function potential by linking taxonomy information with pre-calculated&curated KEGG pathway.Significantly enriched or depleted metabolic pathway were summarized and visualized in heatmap after all unreasonable metabolic pathways were excluded from the dataset.

**PS** Just as a reference, as some of the analysis were documented as CV1(WIL), CV2(DRT), CV3(CNR), CV4(NNW), CV5(SOJ) and CV6(W82).

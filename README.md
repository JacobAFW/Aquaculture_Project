# Environmental factors affecting seasonality of ciliate parasite and bacterial microbiome in a marine fish farm from Hong Kong.

This repository contains the analysis for a project exploring the relationship between the parasite Cryptocaryon and both the aquatic bacterial microbiome (16S rRNA gene amplicon sequencing) and a collection of environmental parameters (collected over several months).

The analyses were conducted using R Studio Version 3.6.1 with a pipeline based on a workflow from the paper [Characterising the bacterial gut microbiome of probiotic-supplmented very-preterm infants](https://github.com/JacobAFW/NICU_Microbiome_Study/blob/main/Complete_Workflow_NICU_Microbiome.pdf) and the [DADA2](https://pubmed.ncbi.nlm.nih.gov/27508062/) workflow developed by *Callahan, et al.*. *DADA2* was used for quality filtering and trimming, demultiplexing, denoising and taxonomic assignment (using the *SILVA* Database). *microDecon*  was used for contamination removal from samples using blanks. A *phyloseq* object was created for organising and analysing the data, with taxa filtered by prevalence (threshold = 0.01) and agglomerated at the genus level. 

Heatmaps were use to explore potential associations between both water quality parameters and Cryptocaryon abundance (eDNA) with the bacterial microbiome of water samples. The first heatmap explored the correlation of genera and variables. Genera were normalised with `DESeq2()` (variance stabilising transformation), and subset to the top twenty most abundant taxa. Transformed counts were combined with water quality data and a correlation matrix was created using Kendall’s Tau non-parametric rank correlation with the `cor()` function. `pheatmap()` was then used to create a heatmap from the correlaiton matrix, with clustering by rows/taxonomy. A second heatmap was created to compare abundances of the top twenty taxa between high and low abundance of Cryptocaryon. Again, *DESeq2*-normalised counts for the top20 taxa were used, and a matrix created with the mean abundances for each level in Cryptocaryon abundance (high vs low). `pheatmap()` was again used with clustering by taxonomy. The final heatmap, applied the same method previously described, but only to those taxa deemed to be significantly different between high and low Cryptocaryon abundance by *DESeq2* differential abundance analysis.


A generalised logistic regression model (binomial) was used to explore the effect of both the microbiome and water quality parameters on Cryptocaryon abundance (high vs low) using *lme4*'s `glmer()`. Negative-binomial modelling with *DESeq2* was used (likelihood ratio test) to identify genera associated with Cryptocaryon abundance. Then, both the resulting *DESeq2*-normalised counts and water quality parameters were centred and scaled to avoid convergence issues, and multicollinearity assessed, and collinear variables subsequently removed. An initial optimal model was created with, which subsequently went through backwards selection find the least complex adequate model. The significance of the fixed effects variables in this final model was then assessed using analysis of deviance (Type II Wald Chi-square test) from the *car* package. 

A link to the manuscript will be provided once published.
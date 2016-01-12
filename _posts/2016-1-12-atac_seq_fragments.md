---
title: atac-seq by species continues to be confusing
layout: post
tags: atac-seq
---

The ATAC-seq data appear to have some weird systematic biases in there that I cannot control for. It's clear fragment ratios, and overabundance of 55bp fragments (overdigested?) are driving a lot of the PCA and correlation plots, and are very different between the two species. However, the PCAs are picking up very different trends from the Spearman and Pearson matrices; in the former the main driver of PC1 is the 50/150 ratio, whereas in the latter it's 50/100. There's a few things happening:

* relationships between the covariates
* relationships between the covariates and the actual data

Fragment abundance ratios, before and after merge. The chimp NFR is definitely messed up relative to the human one:
![tss_after_merge_no low cell counts remove over 5_covariates_by_species_ dragged pdf](https://cloud.githubusercontent.com/assets/1609166/12260971/3934b998-b959-11e5-8220-285729fcb0ed.png)
![tss_before_merge_no low cell counts remove over 5_covariates_by_species_ dragged pdf](https://cloud.githubusercontent.com/assets/1609166/12260978/3960dbfe-b959-11e5-94ba-64db674f26fc.png)

![tss_after_merge_no low cell counts remove over 5_covariates_by_species_ dragged _1 pdf](https://cloud.githubusercontent.com/assets/1609166/12260970/39339d60-b959-11e5-830c-838698c2deab.png)
![tss_before_merge_no low cell counts remove over 5_covariates_by_species_ dragged _1 pdf](https://cloud.githubusercontent.com/assets/1609166/12260977/396018f4-b959-11e5-8313-1b4fae571999.png)

![tss_after_merge_no low cell counts remove over 5_covariates_by_species_ dragged _2 pdf](https://cloud.githubusercontent.com/assets/1609166/12260968/3932a7de-b959-11e5-847b-6debd7153d7e.png)
![tss_before_merge_no low cell counts remove over 5_covariates_by_species_ dragged _2 pdf](https://cloud.githubusercontent.com/assets/1609166/12260974/395c07e6-b959-11e5-9e81-fe88a6f345fd.png)

![tss_after_merge_no low cell counts remove over 5_covariates_by_species_ dragged _3 pdf](https://cloud.githubusercontent.com/assets/1609166/12260969/39333ad2-b959-11e5-8c56-27f780b28d68.png)
![tss_before_merge_no low cell counts remove over 5_covariates_by_species_ dragged _3 pdf](https://cloud.githubusercontent.com/assets/1609166/12260975/395c7136-b959-11e5-8f2d-3393bfba74c6.png)

Reads in the TSS and BG:
![tss_after_merge_no low cell counts remove over 5_covariates_by_species_ dragged _4 pdf](https://cloud.githubusercontent.com/assets/1609166/12260973/393781d2-b959-11e5-9635-01c91c32338f.png)
![tss_before_merge_no low cell counts remove over 5_covariates_by_species_ dragged _4 pdf](https://cloud.githubusercontent.com/assets/1609166/12260979/3963c9cc-b959-11e5-93fb-d4b66e09a6be.png)

![tss_after_merge_no low cell counts remove over 5_covariates_by_species_ dragged _5 pdf](https://cloud.githubusercontent.com/assets/1609166/12260972/39353440-b959-11e5-96be-2218178dd367.png)
![tss_before_merge_no low cell counts remove over 5_covariates_by_species_ dragged _5 pdf](https://cloud.githubusercontent.com/assets/1609166/12260976/395fb9ea-b959-11e5-869d-d42717c91de2.png)


But then, given how robust this trend is, why does species come to the forefront so much more when I sum replicates? Suggests the effect is cancelled out between replicates of the same species, but it is not. Within an individual trends are pretty consistent, suggesting it's a biological effect, but then *why does most of this effect vanish when I sum replicates????* What else is hiding in the before merge data???

Covariates vs PCs, before and after merging - PC1 and PC2 pretty much switch places, and species is now a powerful driver:
![tss_before_merge_no low cell counts remove over 5_cpm_covariates_vs_pcs pdf](https://cloud.githubusercontent.com/assets/1609166/12260076/964e238a-b954-11e5-9c59-90e12ac11262.png)

![tss_after_merge_no low cell counts remove over 5_cpm_covariates_vs_pcs tss all pdf](https://cloud.githubusercontent.com/assets/1609166/12260069/961df426-b954-11e5-82f9-6f84772a15d6.png)

Sample heatmaps with covariate values, before and after merging. Down is clearly driving the heatmap clustering before, but not after. Why????:
![tss_before_merge_no low cell counts remove over 5_cpm_correlation_heatmaps_tss_all pdf](https://cloud.githubusercontent.com/assets/1609166/12260075/964b01a0-b954-11e5-8420-0f9e293a4e6c.png)

![tss_after_merge_no low cell counts remove over 5_cpm_correlation_heatmaps_tss_spearman pdf](https://cloud.githubusercontent.com/assets/1609166/12260067/961a6464-b954-11e5-8721-b721e3241a8a.png)

**ANYHOW IN MORE IMPORTANT NEWS** found a big problem in the summed data analysis. The conclusion that the fragment effect is less pronounced once replicates are summed holds, but the wrong covariates were being regressed and modelled due to a problem in the script:

`merged.fragments <- ddply(fragments, .(sample.names.ind), function(x) colMeans(x[,c(1:5)]))` controls the merging and re-calculating of the fragment size covariates, but `sample.names.ind` was in the reverse order, and so the covariates matrix for the summed data was totally and completely incorrect. The effect is not too terrible in a way because the human data was summarised as chimp data and viceversa for the most part, but it is still terrible, and when I do it right different covariates become important, but still hard to separate from the data. 

To fix the problem, the line becomes: 

```
merged.fragments <- ddply(fragments, .(rev(sample.names.ind)), function(x) colMeans(x[,c(1:5)]))
```




Bonus: commands to batch rename and batch convert images from pdfs dragged out of preview:

```
for i in *; do mv "$i" "`echo $i | tr ' ' '_'`"; sips -s format png $i --out $i.png; done
```
---
title: atac-seq by species continues to be confusing
layout: post
tags: atac-seq
---

The ATAC-seq data appear to have some weird systematic biases in there that I cannot control for. It's clear fragment ratios, and overabundance of 55bp fragments (overdigested?) are driving a lot of the PCA and correlation plots, and are very different between the two species. However, the PCAs are picking up very different trends from the Spearman and Pearson matrices; in the former the main driver of PC1 is the 50/150 ratio, whereas in the latter it's 50/100. There's a few things happening:

* relationships between the covariates
* relationships between the covariates and the actual data

Fragment abundance ratios:

![tss_before_merge_no low cell counts remove over 5_covariates_by_species_50 150 pdf](https://cloud.githubusercontent.com/assets/1609166/12260068/961b5b08-b954-11e5-8d13-2f89fc760be3.png)

![tss_before_merge_no low cell counts remove over 5_covariates_by_species_down pdf](https://cloud.githubusercontent.com/assets/1609166/12260070/962002ca-b954-11e5-979d-7d1d08022488.png)

![tss_before_merge_no low cell counts remove over 5_covariates_by_species_mid pdf](https://cloud.githubusercontent.com/assets/1609166/12260071/9621f210-b954-11e5-81ae-ba7f70f78b05.png)

![tss_before_merge_no low cell counts remove over 5_covariates_by_species_up pdf](https://cloud.githubusercontent.com/assets/1609166/12260074/9647b4dc-b954-11e5-8af8-51de9123fd04.png)

Reads in the TSS and BG:

![tss_before_merge_no low cell counts remove over 5_covariates_by_species_tss all pdf](https://cloud.githubusercontent.com/assets/1609166/12260072/96451fba-b954-11e5-947f-b30bbae7ee5f.png)

![tss_before_merge_no low cell counts remove over 5_covariates_by_species_tss bg pdf](https://cloud.githubusercontent.com/assets/1609166/12260073/9646ae16-b954-11e5-9de0-f6f0d6674edc.png)


Why does most of this effect vanish when I sum replicates? Suggests the effect is flow-cell specific, but it is not, nothing ever clusters by flow cell or by individual. Within an individual trends are pretty consistent, suggesting it's a biological effect, but then *why does most of this effect vanish when I sum replicates????* 

Covariates vs PCs, before and after merging:

![tss_after_merge_no low cell counts remove over 5_cpm_covariates_vs_pcs tss all pdf](https://cloud.githubusercontent.com/assets/1609166/12260069/961df426-b954-11e5-82f9-6f84772a15d6.png)

![tss_before_merge_no low cell counts remove over 5_cpm_covariates_vs_pcs pdf](https://cloud.githubusercontent.com/assets/1609166/12260076/964e238a-b954-11e5-9c59-90e12ac11262.png)

Sample heatmaps with covariate values, before and after merging:

![tss_before_merge_no low cell counts remove over 5_cpm_correlation_heatmaps_tss_all pdf](https://cloud.githubusercontent.com/assets/1609166/12260075/964b01a0-b954-11e5-8420-0f9e293a4e6c.png)

![tss_after_merge_no low cell counts remove over 5_cpm_correlation_heatmaps_tss_spearman pdf](https://cloud.githubusercontent.com/assets/1609166/12260067/961a6464-b954-11e5-8721-b721e3241a8a.png)

**ANYHOW IN MORE IMPORTANT NEWS** found a big problem in the summed data analysis. The conclusion that the fragment effect is less pronounced once replicates are summed holds, but the wrong covariates were being regressed and modelled due to a problem in the script:

`merged.fragments <- ddply(fragments, .(sample.names.ind), function(x) colMeans(x[,c(1:5)]))` controls the merging and re-calculating of the fragment size covariates, but `sample.names.ind` was in the reverse order, and so the covariates matrix for the summed data was totally and completely incorrect. The effect is not too terrible in a way because the human data was summarised as chimp data and viceversa for the most part, but it is still terrible, and when I do it right different covariates become important, but still hard to separate from the data. 

To fix the problem, the line becomes: 

```
merged.fragments <- ddply(fragments, .(rev(sample.names.ind)), function(x) colMeans(x[,c(1:5)]))
```

There's a co


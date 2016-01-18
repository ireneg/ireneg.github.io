---
title: Cleaning up files for centipede again
layout: post
tags: [atac-seq, mscentipede] 
---

Anil managed to reproduce my bug and has updated the code with a fix. 

After talking to Yoav, have reached a few decisions on the data. Chief amongst them, 

* we will now be *filtering all PWM motif sites without a single read 100 bp around the motif*. This is easy to implement, and is now part of `scan.motif.batch.sh`.
* according to Anil, grouping bams from the same individual should not be a problem even if they have slightly different fragmentation patterns, and the less bams that go in, the less parameters that need to be calculated, the speedier the calculation will be, and the less likely to crash.

I also revisited my lab meeting slides once more and realised that C3647 FC1 should maybe have been filtered out, but wasn't being dealt with. According to the qc scripts, it was never filtered out, so I will keep the sample for the time being, but it's worth returning to the QC script to test what was going on there and the effects of adding and removing the sample. It seems like C3647 is a weird sample, without good reproducibility between runs and replicates. C3647 FC1 routinely fails to cluster with the other two replicates, but it does behave closer to the sample mean.

Right now, files/runs being discarded are:

* C3649 FC2 - pca outlier, over fragmented?
* C3651 FC1 - pca, correlation outlier (low depth)
* C40210 FC1 - pca, correlation outlier

* H19114 FC1 - pca, correlation outlier (very low depth)
* H19101 FC1 - pca, correlation outlier (very low depth)
* H20961 FC1 - pca, correlation outlier (very low depth)
* H18489 FC1 and FC2 - grossly over fragmented


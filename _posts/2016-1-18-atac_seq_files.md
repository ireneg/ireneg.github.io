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

* C3649 FC2 - pca outlier, over fragmented? (done)
* C3651 FC1 - pca, correlation outlier (low depth) (done)
* C40210 FC1 - pca, correlation outlier (done)

* H19114 FC4 - pca, correlation outlier (strange flow cell) (done)
* H19101 FC1 - pca, correlation outlier (very low depth) (done)
* H20961 FC1 - pca, correlation outlier (very low depth) (done)
* H18489 FC1 and FC2 - grossly over fragmented 

The command line for cleaning up was variations of

`samtools view -b -R ~/atac_seq/mapped/atac_seq/filtered/read.group.filter.test C3651.merged.nochrM.rmdup.filter.bam > C3651.merged.nochrM.rmdup.filter.cleanRG.bam`

`~/atac_seq/mapped/atac_seq/filtered/read.group.filter.test` simply looks like:

```
[ireneg@spudling23 mapped_filtered]$ more  ~/atac_seq/mapped/atac_seq/filtered/read.group.filter.test 
FC2.LIB1
FC5.LIB1
FC2.LIB2
FC5.LIB2
```

Also this one liner has been very helpful in checking how things are running and the such as I try to filter the files. 

``` 
for i in {1..5}; do motif=`head logs/$i.scan_all.log -n 1 | sed 's/This job has the task ID [0-9]*, and corresponds to //g'` ; ls -lh $motif*final*  ; done
```
---
title: End of my filtering adventures.
layout: post
tags: [atac-seq, mscentipede]
---

Did a test run on 25 PWMs, checking how many motif sites each library/flowcell/ind matched, and found a wonderful relationship between that and sequencing depth. This is independent of tissue, and the best part is, the data from the Greenleaf lab totally fits the curve. So given our sequencing depth, the filtering idea is bust - PWMs begin to saturate at around 55 million reads. 

Relevant code is in `scan.motifs.by.sample.sh` and `pwm_filtering.R`. Here's three sample figures:

![filtered_read_counts_by_ind_by_pwm_ dragged _1 pdf](https://cloud.githubusercontent.com/assets/1609166/12502074/b9b87bd8-c0ff-11e5-882b-e131dfa9efb6.png)

![filtered_read_counts_by_ind_by_pwm_ dragged _2 pdf](https://cloud.githubusercontent.com/assets/1609166/12502073/b9b76e8c-c0ff-11e5-90ca-e06fbf098dc3.png)

![filtered_read_counts_by_ind_by_pwm_ dragged pdf](https://cloud.githubusercontent.com/assets/1609166/12502075/b9b9b3f4-c0ff-11e5-9bf6-2d3ee73a78ad.png)

So, in conclusion:

* filtering: pointless
* collapsing BAMs over individuals: legit, and done
* number of model fittings needed: 3 or 4
* overflow error bug: fake-solved by Anil 

Currently looking into whether I can add an ID column to the bedfile so that I can a. sort the chimp bedfile by genomic position rather than orthology, and b. compare across species less painfully. 

As soon as I hear back from him that the value error has been solved I'll be launching all the jobs again. 
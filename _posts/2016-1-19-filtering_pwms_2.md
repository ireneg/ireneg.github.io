---
title: Filtering PWMs for centipede continued
layout: post
tags: [atac-seq, mscentipede] 
---

While I wait for `scan.motifs.by.sample.sh` to finish running, I've looked at what happens if we limit ourselves to only looking at those motifs with reads 100bp or 50bp around them, instead of the entire motif population. 

The short version is, nothing much:

![filtered_motifs_by_pwm pdf](https://cloud.githubusercontent.com/assets/1609166/12423271/9f3730de-bf05-11e5-92ea-b4e73e60dfb2.png)

Now looking to see if any particular individual is behind this, or if it's simply to be expected. As I said to Shyam:

given the genome is 3 billion bp, and we have between 170-200 million reads, we would expect 1 read randomly every 15-18 bp
but we know not all the genome is open, and we hope the reads aren't randomly distributed throughout the genome (we know they're not, in fact, there's an excess of them in TSSs relative to background)
i'm gonna say those two factors cancel out, because why not
so i guess what we're seeing more or less makes sense, but my god, this is a very noisy assay, then 
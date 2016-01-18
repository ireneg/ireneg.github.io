---
title: Filtering PWMs for centipede
layout: post
tags: [atac-seq, mscentipede] 
---

Further to my previous post I have been playing with `scan.motif.batch.sh` to filter PWM sites to only those with at least one read mapped within 100 bp up or downstream of the PWM motif itself. From the PWMs that have finished it does not seem like this is going to be a very selective approach (on the plus side, the code is working...)

```
[ireneg@spudling10 scanMotif]$ for i in {1..5}; do motif=`head logs/$i.scan_all.log -n 1 | sed 's/This job has the task ID [0-9]*, and corresponds to //g'` ; for j in `ls $motif*gz`; do echo $j; zcat $j | wc -l ;done   ; done
M03978.C.final.bed.gz
2074
M03978.C.final.filter.bed.gz
2073
M03978.H.final.bed.gz
2074
M03978.H.final.filter.bed.gz
2073
M01441.C.final.bed.gz
305352
M01441.C.final.filter.bed.gz
303443
M01441.H.final.bed.gz
305352
M01441.H.final.filter.bed.gz
304487
M05353.C.final.bed.gz
57376
M05353.C.final.filter.bed.gz
57352
M05353.H.final.bed.gz
57376
M05353.H.final.filter.bed.gz
57370
ls: M01392.*gz: No such file or directory
M03935.C.final.bed.gz
13470
M03935.C.final.filter.bed.gz
13449
M03935.H.final.bed.gz
13470
M03935.H.final.filter.bed.gz
13459
```

If I get bored I might try running 1 PWM against each bamfile independently to see if there are some that are way noisier than others, but given how this happens to both the humans and the chimps, I'm not sure what I'll learn. For now I am trying with 50bp instead. 
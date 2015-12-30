---
title: batch submitting mscentipede jobs
layout: post
tags: mscentipede
---

Wrote a script to submit all mscent jobs to the cluster as a single tasked array. However, have exceeded my submission quota and won't be able to test it until the scan.motifs jobs are all done, which is annoying. 

The script seems like it will need debugging, because on qsub the job name is STDIN, which it really shouldn't be, since it's being quite clearly specified with the -N option. I was hoping to start running mscent on small batches of PWMs now, but for that I'd probably have to kill the current scan motif job and launch it with a max number of parallel jobs at once, if it respects that option. 

I guess it gives me time to work on subsetting the human reads...
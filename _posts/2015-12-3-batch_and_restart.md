---
title: testing --batch and --restart
tags: mscentipede, atac-seq
layout: post
---

I set up a bunch of jobs to test the --batch and --restarts flags, testing from 1000 to 20000 motifs. After much fighting with the cluster to avoid the big spudlings (the solution ended up being `-q blades.q`), the results so far are:

* 11 jobs with overflow errors/crashes
* 8 finished jobs
* 41 jobs still running

**Human**

PWM | Sites | 1000 | 5000 | 10000 | 15000 | 20000 | default
----|-------|------|------|-------|-------|-------|--------
M01123 | 308652 | overflow 1 | | | | | overflow 1
M03895 | 17666 | | | | | | finish
M04459 | 128991 | | | | | finish
M04539 | 10484 | | | | | | finish
M04735 | 927059 | finish | | | overflow 1 | | finish
M05589 | 953 | finish | finish | finish | overflow 4 | overflow 5 | finish

**Chimp**

PWM | Sites | 1000 | 5000 | 10000 | 15000 | 20000 | default
----|-------|------|------|-------|-------|-------|--------
M01123 | 308652 | overflow 5 | | | | overflow 1 | finish
M03895 | 17666 | overflow 2 | | overflow 1 | | | finish
M04459 | 128991 | | | | | finish
M04539 | 10484 | | | | | | finish
M04735 | 927059 | overflow 2 | | | overflow 1 | | finish
M05589 | 953 | overflow 1 | finish | finish | finish | finish | finish

Tolerance before the restart was set to the default value, < 1e-6. The default run above was set to 1e-5 instead. 

There seems to be no link between what fails and what works, and the overflow error doesn't always occur at the first iteration, which it should if it's deterministic. However, increasing the number of sites increases (greatly) the iteration time, which is not surprising, but it might come down to being a trade-off between time and robustness?

Things pending:

* Interpreting the final output. 
* This ties in to the fact that I didn't call binding on any of these tests, but I should've, to see how varying the batch parameter affects things. 
* Understanding the restarts flag. Right now I'm still only getting one model at the end of the 5 runs, and it's not clear if it's an optimised model or what is going on there. It must be optimised, because otherwise there's no point to doing any of this, but HOW is the question. 
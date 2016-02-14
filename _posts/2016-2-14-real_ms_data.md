---
title: Real msCentipede run statistics
layout: post
tags: [mscentipede, atac-seq]
---

The speed improvements are making quite a big difference to run times - compare this with the old histogram data from ()[] (this was generated in exactly the same way). I've been doing some on-going QC on the jobs, to be sure nodes don't get held hostage running pointless calculations:

```
setwd("~/Desktop/cluster_sync/")
onion <- read.table("~/Desktop/cluster_sync/iteration_times.txt")
png("iteration_time_hist.png")
hist(onion$V16, xlab="Time (seconds)", main="")
dev.off()

dim(onion)
[1] 18350    17

onion.long <- onion[onion$V16 >= 5000,]

dim(onion.long)
[1] 62 17
length(unique(onion.long$V1))
[1] 11

onion.short <- onion[onion$V16 < 5000,]
dim (onion.short)
[1] 18288    17

summary(onion$V16)
    Min.  1st Qu.   Median     Mean  3rd Qu.     Max. 
   12.72  1944.00  2388.00  2139.00  2557.00 60420.00 
summary(onion.short$V16)
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
  12.72 1939.00 2387.00 2120.00 2555.00 4999.00 
```

These are the 11 PWMs that have taken more than 5000 seconds per iteration at least once. It's hard to decide what to do with the borderline cases, but jobs 605 and 520 were not difficult decisions:

PWM | job id | status
----------------------
M01670.chimp.log | 605 | current model taking 48000 seconds/iteration *KILLED* 
M01780.human.log | 608 | single iteration over 5000 seconeds, usually at 4500
M02288.human.log | 478 | 79 iterations at ~5000 seconds for first model fitting, no sign of convergence 
M04338.chimp.log | 610 | multiple iterations at ~5000 seconds for first model fitting, no sign of convergence 
M04618.human.log | 518 | consistently at >= 5000 seconds for first model fitting, no sign of convergence 
M05373.human.log | 520 | multiple iterations at > 10k seconds *KILLED*
M05540.human.log | 524 | single iteration at 5000 seconds at the beginning of model fitting, usually at 2500 
M05567.human.log | 552 | multiple iterations at ~5000 seconds for first model fitting, no sign of convergence 
M05999.chimp.log | 602 | single iteration at 5000 seconds at the beginning of model fitting, usually at 2500
M06297.human.log | 624 | single iteration at 5000 seconds, already finished and fitted
M06754.chimp.log | 627 | multiple iterations > 5000 in previous round of model fitting

Also checked all jobs with more than 100 iterations. Job 9 was also not a difficult decision:

`grep "iteration 100" *.log`

PWM | job id | status
----------------------
M01195.human.log | 647 | took 964 iterations at around 220 seconds, but finished, and model is now fitted
M01282.human.log | 467 | finished model after 130 iterations
M01351.human.log | 631 | 110 iterations at 2500 seconds each for first model fitting, no sign of converging
M01352.human.log | 485 | 136 iterations at 2500 seconds each for first model fitting, no sign of converging
M02756.human.log | 489 | 137 iterations at 2500 seconds each for first model fitting, last few iterations at around 9e-5
M04003.human.log | 9 | 200+ iterations at 2500 seconds each and no sign of convergence. *KILLED*
M04008.human.log | 19 | 108 iterations at 2500 seconds each for first model fitting, likelihoods generally around 1e-4
M04211.human.log | 14 | finished model after 106 iterations
M04242.human.log | 649 | finished model after 158 iterations
M04534.human.log | 630 | finished model after 137 iterations
M05362.human.log | 621| 104 iterations at 2500 seconds each for first model fitting, no sign of converging
M05407.human.log | 488 | 121 iterations at 2500 seconds each for second model fitting, first model converged after 10 
M05515.human.log | 629 | 102 iterations at 2500 seconds each for first model fitting, no sign of converging
M06754.human.log | 627 | 112 iterations at 2300 seconds each for first model fitting, last few iterations at 5e-5
M06884.human.log | 511 | finished model after 298 iterations 
M07341.human.log | 619 | 108 iterations at 2400 seconds each for first model fitting, no sign of converging


---
title: tracking slow jobs
layout: post
tags: [mscentipede]
---

A few more jobs overnight with too many bad iterations:

PWM | job id | status 
----|--------|--------
M01147.human.log | 519 | 112 iterations at 2500 seconds each for first model fitting, no sign of converging
M04315.human.log | 454 | 111 iterations at 3400 seconds each for first model fitting, no sign of converging
M04242.human.log | 649 | 100+ iterations AGAIN
M04422.human.log | 532 | finished model after 102 iterations
M05515.human.log | 629 | 127 iterations at 2500 seconds each for first model fitting, no sign of converging
M06984.human.log | 577 | 100+ iterations in two runs so far at 130 seconds each, converges well
M07341.human.log | 619 | 134 iterations at 2400 seconds each for first model fitting, no sign of converging

Pending problematic [jobs from yesterday](http://ireneg.github.io/real_ms_data/) that I control + any new jobs that slipped into 100 iterations overnight + jobs that have been running since I first launched the scripts (job ID 1-20 or 450-500) and what I have done to all of those:

PWM | job id | status | outcome
----|--------|--------|--------
M04003.human.log | 9 | 200+ iterations at 2500 seconds each and no sign of convergence | **KILLED**
M04211.human.log | 14 | finished model after 106 iterations. Slow job, but rinning well. Finishing 4th fitting | **RUNNING**
M04050.human.log | 18 | slow job, but running well. Finishing 5th fitting | **RUNNING**
M04008.human.log | 19 | 108 iterations at 2500 seconds each for first model fitting, likelihoods generally around 1e-4 | **KILLED**
M05927.human.log | 461 | slow job, but running well. Finishing 3rd fitting | **RUNNING**
M01282.human.log | 467 | finished model after 130 iterations. Slow job, running 2nd fitting now | **RUNNING**
M01482.human.log | 469 | slow job, but running well. Finishing 3rd fitting | **RUNNING**
M02288.human.log | 478 | 79 iterations at ~5000 seconds for first model fitting, no sign of convergence | **KILLED**
M07205.human.log | 480 | slow job, but running well. Finishing 3rd fitting | **RUNNING**
M01352.human.log | 485 | 136 iterations at 2500 seconds each for first model fitting, no sign of converging | **finished @ 148 iterations**
M05407.human.log | 488 | 121 iterations at 2500 seconds each for second model fitting, first model converged after 10 | **KILLED**
M02756.human.log | 489 | 137 iterations at 2500 seconds each for first model fitting, last few iterations at around 9e-5 | **finished @ 153 iterations**
M00165.human.log | 492 | slow job, but running well. Finishing 3rd fitting | **RUNNING**
M01401.human.log | 494 | slow job, but running well. Finishing 2nd fitting | **RUNNING**
M06884.human.log | 511 | finished model after 298 iterations | **FULLY FINISHED**
M04618.human.log | 518 | consistently at >= 5000 seconds for first model fitting, no sign of convergence | **KILLED**
M05373.human.log | 520 | multiple iterations at > 10k seconds | **KILLED**
M05567.human.log | 552 | multiple iterations at ~5000 seconds for first model fitting | **finished overnight**
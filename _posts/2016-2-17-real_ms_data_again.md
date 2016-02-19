---
title: Real msCentipede run statistics update
layout: post
tags: mscentipede
---

10 days after starting the launch, some summary stats:

```
for i in {1..5}; do grep "restart $i" *.log | wc -l ; done
331
298
270
41
40
ls -lh *gz | wc -l
241
```

As for cleaning up, all pending problematic jobs from previous post. Note that I can't do anything about jobs > 600:

PWM | job id | status | outcome
----|--------|------------------
M04211.human.log | 14 | 4th fitting at 108 iterations so far, previous one finished at 106 | **RUNNING**
M04050.human.log | 18 | slow job, but running well. Finishing 5th fitting | **FINISHED**
M04315.human.log | 454 | 158 iterations at 3400 seconds each for SECOND (whoops) model fitting, no sign of converging | **KILLED**
M05927.human.log | 461 | slow job, but running well. Finishing 3rd fitting | **FINISHED**
M01282.human.log | 467 | finished model after 130 iterations. Slow job, running 2nd fitting now | **FINISHED**
M01482.human.log | 469 | slow job, but running well. Finishing 3rd fitting | **FINISHED**
M07205.human.log | 480 | STILL Finishing 3rd fitting | **RUNNING**
M00165.human.log | 492 | slow job, but running well. Finishing 3rd fitting | **FINISHED**
M01401.human.log | 494 | Finishing 3rd fitting | **RUNNING**
M01147.human.log | 519 | 174 iterations at 2500 seconds each for first model fitting, no sign of converging | **KILLED**
M04422.human.log | 532 | finished model after 102 iterations. Finishing 3rd fitting | **RUNNING**
M06984.human.log | 577 | 100+ iterations in two runs so far at 130 seconds each, converges well | **FINISHED**
M07341.human.log | 619 | 201 iterations at 2400 seconds each for first model fitting, no sign of converging | **RUNNING**
M05515.human.log | 629 | 191 iterations at 2500 seconds each for first model fitting, no sign of converging | **RUNNING**
M04242.human.log | 649 | 100+ iterations for the third time, but always converges around this number | **RUNNING**

New jobs with more than 100 iterations and slow jobs (human job ID 500-550). Note that I can't do anything about jobs > 600:

PWM | job id | status | outcome
----|--------|------------------
M04861.human.log | 522 | 148 iterations at 2200 seconds each for second model fitting, finished first at 35. No sign of converging | **RUNNING** 
M04544.human.log | 545 | 189 iterations at 1800 seconds each for first model fitting, no sign of converging | **RUNNING** 
M06631.human.log | 547 | 141 iterations at 2400 seconds each for first model fitting, no sign of converging | 
M06754.human.log | 627 | finished model after 144 iterations. Running 2nd fitting now | **RUNNING** 
M06993.human.log | 636 | 126 iterations at 2200 seconds each for third model fitting, finished previous one at ~30. No sign of converging | **RUNNING** 
M01370.chimp.log | 650 | 111 iterations at 2200 seconds each for first model fitting, no sign of converging | **RUNNING** 
M01370.human.log | 650 | 114 iterations at 4200 seconds each for first model fitting, no sign of converging | **RUNNING** 
M04404.human.log | 611 | 120 iterations at 4000 seconds each for first model fitting, no sign of converging | **RUNNING**
M04534.chimp.log | 630 | finished model after 115 iterations. Running 2nd fitting now | **RUNNING** 
M04534.human.log | 630 | finished models after 123 and 138 iterations. Running 3rd fitting now | **RUNNING**
M05362.human.log | 621 | finished model after 125 iterations. Running 2nd fitting now | **RUNNING** 
M06245.human.log | 517 | slow job but running well, finishing 3rd model fitting | **RUNNING** 
M04161.human.log | 526 | slow job but running well, finishing 3rd model fitting - seems to have restarted the first fitting twice? Fail to converge? | **RUNNING**
M01472.human.log | 537 | 84 iterations at 4800 seconds each for first model fitting, no sign of converging | **RUNNING**
M00290.human.log | 538 | 88 iterations at 2400 seconds each for third model fitting, finished previous one at ~30. | **RUNNING**
M04186.human.log | 546 | slow job but running well, finishing 3rd model fitting | **RUNNING**
M03957.human.log | 548 | slow job but running well, finishing 3rd model fitting | **RUNNING**

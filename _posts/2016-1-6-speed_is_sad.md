---
title: msCentipede speed woes
layout: post
tags: mscentipede
---

msCentipede continues to misbehave, but in a somewhat predictable fashion, I guess?

After over 5 days running, only 6 PWMs have finished running. I've noticed that a lot of the PWMs take FOREVER to run, with a mean iteration time of around 5000 seconds, around 1.5 hours. That's a long time, considering we're doing 25220 model fittings... 

So I went into the cluster and dug around a bit:

`grep "iteration" *.log > iteration_times.txt` gave me all the iteration times in the PWMs that have not yet crashed, both finished and unfished. From there, into R:

```
onion <- read.table("~/Desktop/cluster_temp/iteration_times.txt")
png("iteration_time_hist.png")
hist(onion$V16, xlab="Time (seconds)", main="")
dev.off()
```

The histogram confirms my hunch that there's a bimodal distribution of speeds, with slow PWMs and fast ones:

![iteration_time_hist](https://cloud.githubusercontent.com/assets/1609166/12135804/681c3d9a-b47b-11e5-882f-5f71009d85b4.png)

The finished ones are obviously fast ones, as can be seen in this plot of mean iteration time by PWM. In red are the ones that are done, which are easily found by doing `ls *.pkl` in the output directory and then going back into R:

```
finished <- "M03978|M06899|M04499|M06164|M06745|M05968"
blah <- ifelse(grepl(finished,levels(onion$V1)), 2, 1)
png("mean_iteration_time.png")
plot(as.vector(unlist(by(onion, as.factor(onion$V1), function(x) mean(x$V16)))), col=blah)
dev.off()
```

![mean_iteration_time](https://cloud.githubusercontent.com/assets/1609166/12135843/1a70111a-b47c-11e5-8973-46266f96f666.png)

Similarly interesting are the super slow PWMs:

``` which(unlist(by(onion, as.factor(onion$V1), function(x) mean(x$V16))) >= 7000)
M00984.human.log:iteration M01392.human.log:iteration M06351.human.log:iteration M06950.human.log:iteration 
                         5                          8                         49                         58 
M07141.human.log:iteration 
                        62 
```

Having done that, one can grep the PWMs that have finished (`grep 'M03978\|M06899\|M04499\|M06164\|M06745\|M05968' ~/atac_seq/reference/centipede/high_ic_transfac_pwms.txt`) and the slowest PWMs of them all (`grep 'M07141\|M00984\|M01392\|M06351\|M06950' ~/atac_seq/reference/centipede/high_ic_transfac_pwms.txt`), and in turn look those up in ENCODE H1 expression data, where it turns out there's no obvious link between expression level and speed of model learning, which was my favourite explanation:

![screen shot 2016-01-06 at 13 48 57](https://cloud.githubusercontent.com/assets/1609166/12135857/4b055cea-b47c-11e5-95ad-17afd2d86597.png)

However, there's a far more sensible one, which is the information content of the PWMs.


```
pwms <- read.table("high_ic_transfac_pwms.txt")
onion$pwm <- gsub(".human.log:iteration", "", onion$V1)
filt.pwm <- pwms[pwms$V1 %in% onion$pwm,]
filt.pwm <- filt.pwm[order(as.character(filt.pwm$V1)),]
onion <- onion[order(as.character(onion$pwm)),]
finished <- "M03978|M06899|M04499|M06164|M06745|M05968"

png(file="iteration_time_vs_genomic_hits.png")
plot(filt.pwm[filt.pwm$V1 %in% onion$pwm,5] ~ as.vector(unlist(by(onion, as.factor(onion$pwm), function(x) mean(x$V16)))), col=ifelse(grepl(finished, filt.pwm$V1), 2, 1), xlab="Mean iteration time (s)", ylab="Genomic PWM motif matches", pch=16)
legend(x="topright", legend=c("Finished", "Running"), pch=16, col=c(2,1))
dev.off()

png(file="iteration_time_vs_ic.png")
plot(filt.pwm[filt.pwm$V1 %in% onion$pwm,4] ~ as.vector(unlist(by(onion, as.factor(onion$pwm), function(x) mean(x$V16)))), col=ifelse(grepl(finished, filt.pwm$V1), 2, 1), xlab="Mean iteration time (s)", ylab="PWM information content", pch=16)
legend(x="topright", legend=c("Finished", "Running"), pch=16, col=c(2,1))
dev.off()
```

![iteration_time_vs_genomic_hits](https://cloud.githubusercontent.com/assets/1609166/12136864/cfab5116-b486-11e5-8df5-378b56c5a44d.png)

Do note that the number of motif hits here is actually the number of hits that pass filtering according to Anil's criteria, and does not reflect the number we're testing across human and chimp (I should try to put that list together)

![iteration_time_vs_ic](https://cloud.githubusercontent.com/assets/1609166/12136865/cfd763dc-b486-11e5-9140-46fb1b9540bf.png)

So, I'll be emailing people about this and seeing where we decide to go from there. 






---
title: msCentipede speed woes continued
layout: post
tags: mscentipede
---

Continuing my msCentipede troubleshooting adventures, here go another few figures I made to write back to Anil. 

```
setwd("~/Data/atac_seq/")
pwms <- read.table("high_ic_transfac_pwms.txt")
overflow <- read.table("overflow_errors.txt")
finished <- read.table("finished_pwms.txt")

overflow$pwm <- gsub(".human.centipede.log:OverflowError:", "", overflow$V1)
finished <- read.table("finished_pwms.txt")
finished <- gsub(".human.pkl", "", finished$V1)

pwms$col <- ifelse(pwms$V1 %in% finished, 2, 1)
pwms[overflow$pwm,6] <- 3
small.pwm <- pwms[1:100,]
```

(filtered to the top 100 PWMs, because we haven't started running anything beyond that, so there's no point looking at it)

First off, it's quite clear that IC is the explanation here. The second plot shows it better than the first, but the relationship is strong in either. 

```
png("pwm_vs_ic.png")
plot(small.pwm$V4[1:100], pch=16, col=small.pwm$col, xlab="PWM", ylab="IC")
legend(x="bottomright", legend=c("Running", "Finished", "Overflow"), col=c(1,2,3), pch=16)
dev.off()

png("ic_by_status.png")
boxplot(small.pwm$V4 ~ as.factor(small.pwm$col), ylab="PWM IC", names=c("Running", "Finished", "Overflow"))
dev.off()
```

![pwm_vs_ic](https://cloud.githubusercontent.com/assets/1609166/12161626/e9ff1fa0-b532-11e5-8998-1a4eadc5394d.png)

![ic_by_status](https://cloud.githubusercontent.com/assets/1609166/12161625/e9fc73ea-b532-11e5-8a78-f9aa9ca41a4b.png)


The one beneath is presumably the least helpful of all the analyses, because the boxplot doesn't show how many motifs there are in each category (the differences are vast), and because it's only two of each, but pairwise T-testing all around (not shown) suggests that the two that finished had far more informative motifs than the ones that did not finish.  

```
finish1 <- read.table("M03978.H.final.bed")
overflow1 <- read.table("M01714.H.final.bed")
finish2 <- read.table("M05552.H.final.bed")
overflow2 <- read.table("M06641.H.final.bed")
onion <- list(finish1, finish2, overflow1, overflow2)

png("finish_vs_overflow_boxplots.png")
boxplot(onion, names=c("Finish1", "Finish2", "Overflow1", "Overflow2"), ylab="motif PWM score")
dev.off()
```

![finish_vs_overflow_boxplots](https://cloud.githubusercontent.com/assets/1609166/12161624/e9fb2404-b532-11e5-98e7-dbecca1e6d19.png)
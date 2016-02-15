---
title: msCentipede running for realz.
layout: post
tags: [mscentipede, atac-seq]
---

msCentipede is now running on all atac-seq data, albeit very slowly. From talking to Anil, decided to merge bam files across flow cells for every individual, so that there's six files for the humans and seven for the chimps, one per ind. Read depths are around 200 million for human, around 170 for chimp. 

Also sorted the chimpanzee input bed files so they're ordered by chr:pos, which has really sped things up on that side. As noted in `scan.motifs.batch.sh`: 

> Chimps and humans are treated differently; there are three chimp files (sorted relative to human orhtology, sorted internally, and for msCentipede) vs the two human files. 

The extra files will make matching PWM sites easy, since talking to both Anil and Shyam, it seems like modifying the msCentipede code so it can handle bed6 input instead of bed5 was just not worth the effort. 

Jobs were submitted in batches of 150, which lets me have matching human and chimp data sooner - Shyam is supposedly handling 601-1261; I've submitted 1-600 with 5gb each, can run about 60/day. Number of model fitting iterations is now down to 3 from a rather unrealistic 10; if I had access to more nodes I would run more, but there's nothing to be done here. As it is, about 10-20 jobs, no more, finish per day, so this is already going to take quite a while. There has to be a way to speed things up, or we will never finish! I think at this point the only other convincing speed ups will come from dropping individuals, which it might be worth doing - the more bam files, the more parameters that need to be calculated in the optimisation step, from what I gather from Anil, so dropping some should speed things up. Or we could fit a single iteration of the model, but I really don't like that. 
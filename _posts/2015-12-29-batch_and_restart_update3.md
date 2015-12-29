---
title: latest batch and restart update
layout: post
tags: mscentipede
---

Spent the past two weeks pursuing mostly admin dead ends, but now it is back to ATAC-seq. After all this time (and still waiting for answers to questions detailed in previous posts), the situation is:

After 26 days, 60 jobs total, of which:
    
* 32 finished
* 18 overflow error
* 1 domain name error
* 9 still running

**Human**

| PWM    | Sites | 1000       | 5000       | 10000  | 15000        | 20000      | default |
|:-------|------:|:----------:|:----------:|:------:|:------------:|:----------:|:-----------:|
| M01123 |308652 | overflow 1 | finish     | finish | finish       | finish     | overflow 1 |
| M03895 |17666  | finish     | finish     | finish | finish       | overflow 3 | finish |
| M04459 |128991 | -          | overflow 2 | -      | -            | -          | finish |
| M04539 |10484  | -          | finish     | -      | -            | -          | finish |
| M04735 |927059 | finish     | finish     | finish | overflow 1   | overflow 2 | finish |
| M05589 |953    | finish     | finish     | finish | domain error | overflow 5 | finish |

**Chimp**

| PWM    | Sites | 1000       | 5000       | 10000      | 15000      | 20000      | default |
|:-------|------:|:----------:|:----------:|:----------:|:----------:|:----------:|:-----------:|
| M01123 |308652 | overflow 5 | overflow 4 | overflow 4 | finish     | overflow 1 | finish | 
| M03895 |17666  | overflow 2 | finish     | overflow 1 | finish     | finish     | finish |
| M04459 |128991 | -          | finish     | finish     | overflow 5 | finish     | finish |
| M04539 |10484  | finish     | finish     | finish     | finish     | finish     | finish |
| M04735 |927059 | overflow 2 | finish     | finish     | overflow 1 | finish     | finish |
| M05589 |953    | overflow 1 | finish     | finish     | finish     | finish     | overflow 1 |


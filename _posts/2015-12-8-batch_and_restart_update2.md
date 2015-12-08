---
title: more batch and restart
layout: post
tags: mscentipede
---

Some progress overnight, but some runs are still running real long... 

After six days, 60 jobs total, of which:

* 18 finished
* 14 overflow error
* 1 domain name error
* 27 still running

**Human**

| PWM    | Sites | 1000       | 5000   | 10000  | 15000        | 20000      | default |
|:-------|------:|:----------:|:------:|:------:|:------------:|:----------:|:-----------:|
| M01123 |308652 | overflow 1 | -      | finish | -            | -          | overflow 1 |
| M03895 |17666  | -          | finish | finish | finish       | overflow 3 | finish |
| M04459 |128991 | -          | -      | -      | -            | -          | finish |
| M04539 |10484  | -          | -      | -      | -            | -          | finish |
| M04735 |927059 | finish     | finish | finish | overflow 1   | overflow 2 | finish |
| M05589 |953    | finish     | finish | finish | domain error | overflow 5 | finish |

**Chimp**

| PWM    | Sites | 1000       | 5000       | 10000      | 15000      | 20000      | default |
|:-------|------:|:----------:|:----------:|:----------:|:----------:|:----------:|:-----------:|
| M01123 |308652 | overflow 5 | overflow 4 | overflow 4 | -          | overflow 1 | finish | 
| M03895 |17666  | overflow 2 | finish     | overflow 1 | -          | -          | finish |
| M04459 |128991 | -          | -          | -          | -          | -          | finish |
| M04539 |10484  | finish     | finish     | -          | -          | -          | finish |
| M04735 |927059 | overflow 2 | finish     | -          | overflow 1 | -          | finish |
| M05589 |953    | overflow 1 | finish     | finish     | finish     | finish     | overflow 1 |


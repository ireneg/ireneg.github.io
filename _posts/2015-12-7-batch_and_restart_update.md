---
title: batch and restart updated
layout: post
tags: mscentipede
---

An update on the output, after five days of running:

60 jobs total, of which:

* 13 finished
* 14 overflow error
* 1 domain name error
* 32 still running

**Human**

| PWM    | Sites | 1000       | 5000   | 10000  | 15000        | 20000      | default |
|:-------|------:|:----------:|:------:|:------:|:------------:|:----------:|:-----------:|
| M01123 |308652 | overflow 1 | -      | -      | -            | -          | overflow 1 |
| M03895 |17666  | -          | finish | -      | -            | overflow 3 | finish |
| M04459 |128991 | -          | -      | -      | -            | -          | finish |
| M04539 |10484  | -          | -      | -      | -            | -          | finish |
| M04735 |927059 | finish     | finish | -      | overflow 1   | overflow 2 | finish |
| M05589 |953    | finish     | finish | finish | domain error | overflow 5 | finish |

**Chimp**

| PWM    | Sites | 1000       | 5000       | 10000      | 15000      | 20000      | default |
|:-------|------:|:----------:|:----------:|:----------:|:----------:|:----------:|:-----------:|
| M01123 |308652 | overflow 5 | overflow 4 | overflow 4 | -          | overflow 1 | finish | 
| M03895 |17666  | overflow 2 | finish     | overflow 1 | -          | -          | finish |
| M04459 |128991 | -          | -          | -          | -          | -          | finish |
| M04539 |10484  | finish     | -          | -          | -          | -          | finish |
| M04735 |927059 | overflow 2 | finish     | -          | overflow 1 | -          | finish |
| M05589 |953    | overflow 1 | finish     | finish     | finish     | finish     | overflow 1 |

Shyam has failed to debug the code that returns the overflow error and, last I knew, was contacting Anil about it. 

Of the ones running, some have reached ridiculous numbers of iterations and are clearly failing to converge efficiently, eg:

```
==> M01123.5000.human.log <==
iteration 65: log likelihood = -7.25e+01, change in log likelihood = 5.55e-06, iteration time = 5343.897 secs
==> M03895.1000.human.log <==
iteration 785: log likelihood = -3.45e+02, change in log likelihood = 1.69e-06, iteration time = 509.400 secs
==> M04459.1000.human.log <==
iteration 557: log likelihood = -4.85e+01, change in log likelihood = 8.41e-05, iteration time = 718.181 secs
```

:frowning:


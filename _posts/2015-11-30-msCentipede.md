---
layout: post
title: msCentipede notes 15.30.11
---

1. msCentipede apparently needs to be run locally from /bin/? Was having problems on Fri queueing it all up outside the directory, failing to find the right modules:

```
[ireneg@spudling77 logs]$ tail M01123.c.centipede.out
    import cvxopt as cvx
ImportError: No module named cvxopt
Predicting binding in chimps for motif M01123.
Traceback (most recent call last):
  File "/mnt/gluster/home/ireneg/bin/msCentipede/call_binding.py", line 5, in <module>
    import mscentipede
  File "mscentipede.pyx", line 5, in init mscentipede (mscentipede.c:30355)
    import cvxopt as cvx
ImportError: No module named cvxopt
ERROR: Failed to estimate binding for M01123 in chimps with error code 1
``` 

2. The sixth column in the bed file - the PWM id - also causes msCentipede to fail. Have to reprocess all the files to remove that column - should only do it before gzipping the final final bed that only msCentipede will see. 

3. Aparently github markdown has a different code block code? Srsly? ugh. 

4. Sorry, rather than ugh I meant :unamused:

---
title: mscentipede on real human data
layout: post
tags: mscentipede
---

Over the weekend I launched msCentipede on all 1261 human PWMs. With 5gb of RAM it's taken over 48 hours to do one model run (we're doing 10 to get a good fit; Anil recommended 4-6gb), and iterations are taking about two hours each for most PWMs. Since I can only run around 60 jobs at once, it will take a long long time until this is done, and in the meantime I can't ql into the cluster because I'm flust against my 300 GB RAM quota. So that's that.

Have had a combination of 17 overflow/domain errors so far, with different flavours. I get the feeling some of these will be reproducible, probably, since it seems to be a matrix problem:

```
[ireneg@spudhead logs]$ grep "Overflow" *
11.human.centipede.log:OverflowError: (34, 'Numerical result out of range')
12.human.centipede.log:OverflowError: (34, 'Numerical result out of range')
13.human.centipede.log:OverflowError: (34, 'Numerical result out of range')
17.human.centipede.log:OverflowError: (34, 'Numerical result out of range')
21.human.centipede.log:OverflowError: (34, 'Numerical result out of range')
23.human.centipede.log:OverflowError: (34, 'Numerical result out of range')
3.human.centipede.log:OverflowError: (34, 'Numerical result out of range')
40.human.centipede.log:OverflowError: (34, 'Numerical result out of range')
58.human.centipede.log:OverflowError: (34, 'Numerical result out of range')
61.human.centipede.log:OverflowError: (34, 'Numerical result out of range')
66.human.centipede.log:OverflowError: (34, 'Numerical result out of range')
79.human.centipede.log:OverflowError: (34, 'Numerical result out of range')
8.human.centipede.log:OverflowError: (34, 'Numerical result out of range')
```

and 

```
[ireneg@spudhead logs]$ grep "Value" *
18.human.centipede.log:ValueError: domain error
37.human.centipede.log:    raise ValueError("Rank(A) < p or "\
37.human.centipede.log:ValueError: Rank(A) < p or Rank([H(x); A; Df(x); G]) < n
49.human.centipede.log:    raise ValueError("Rank(A) < p or "\
49.human.centipede.log:ValueError: Rank(A) < p or Rank([H(x); A; Df(x); G]) < n
62.human.centipede.log:    raise ValueError("Rank(A) < p or "\
62.human.centipede.log:ValueError: Rank(A) < p or Rank([H(x); A; Df(x); G]) < n
```
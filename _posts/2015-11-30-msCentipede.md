---
layout: post
title: msCentipede notes 15.30.11
tags: mscentipede
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

**update this appear to be case, at least before trying to qsub. not quite sure how well that will work.**

2. The sixth column in the bed file - the PWM id - also causes msCentipede to fail. Have to reprocess all the files to remove that column - should only do it before gzipping the final final bed that only msCentipede will see. **update this is indeed the case**

3. Aparently github markdown has a different code block code? Srsly? ugh. 

4. Sorry, rather than ugh I meant :unamused:

5. Solved problems 1 and 2. New problem instead:

```
[ireneg@spudling23 msCentipede]$ python call_binding.py --task learn --protocol ATAC_seq --model msCentipede --mintol 1e-5  /mnt/gluster/data/internal_supp/atac_seq/reference/centipede/scanMotif/tester.bed.gz /mnt/gluster/home/ireneg/atac_seq/centipede/mapped_filtered/H19114.merged.nochrM.rmdup.filter.TAG_RG_FC2.LIB1.bam.bai
loading motifs ... 
num of motif sites = 952
loading read counts ... 
Traceback (most recent call last):
  File "call_binding.py", line 344, in <module>
    main()
  File "call_binding.py", line 337, in main
    learn_model(options)
  File "call_binding.py", line 68, in learn_model
    bam_handles = [load_data.BamFile(bam_file, options.protocol) for bam_file in options.bam_files]
  File "/mnt/gluster/home/ireneg/bin/msCentipede/load_data.py", line 82, in __init__
    self._handle = pysam.Samfile(filename, "rb")
  File "csamtools.pyx", line 463, in csamtools.Samfile.__cinit__ (pysam/csamtools.c:4758)
  File "csamtools.pyx", line 601, in csamtools.Samfile._open (pysam/csamtools.c:6290)
ValueError: file does not have valid header (mode='rb') - is it SAM/BAM format?
```
Last I checked everything had been indexed and formatted correctly, and I did in fact manage to get this darned thing to run once with a different test data set, but something must've changed in the interim. 

**Update something seems to have been wrong with the first file I tried; I tried a different one and the following command worked no problem, at least to the point of loading the reads:**

```
python call_binding.py --task learn --protocol ATAC_seq --model msCentipede --mintol 1e-5  /mnt/gluster/data/internal_supp/atac_seq/reference/centipede/scanMotif/tester.bed.gz /mnt/gluster/home/ireneg/atac_seq/centipede/mapped_filtered/H19101.merged.nochrM.rmdup.filter.TAG_RG_FC2.LIB2.bam
```
---
layout: post
title: msCentipede first run
---

msCentipede ran overnight, and have now called binding on a couple of PWMs. Some notes:

1. output is gzipped/pickled. I somehow missed that/it's not documented, so I will have to change file names in script. **update DONE, although just for visual convenience**

2. chimps are far slower than humans - probably due to having more data. After 16 hours running not a single chimp pwm is done and none of the log likelihoods appears ready to converge. There's a lot of PWMs out there, so this might be a big problem...
  - maybe thin the chimps out so there's the same number of reads involved? the number of bound sites is the same, so either the data quality is worse or...
  - **update: the only PWM finished, CTCF, took six hours longer in chimp than human. 13 hours in human, 19 in chimp, ~50% increase in time. will keep checking.**
  - ** update #2: the recovered CTCF footprint is very similar between human and chimp, and in both cases ressembles the real CTCF footprint

3. now looking for scripts to plot the results and check the footprint shape. 

4. the need to run the script from ~/bin could probably be solved by adding a few more things to my path, but I don't quite know which ones and can't be bothered to find out right now. **update probably RESOLVED after having to add twenty different locations to $PYTHONPATH
  - this did highlight how terrible the cluster set up is wrt python. msCentipede is currently running (after Anil) on python 2.6, but some of the libraries it needs are missing unless I add what appears to be a bunch of python 2.7 paths to PYTHONPATH.**
  - this also did highlight how much i need to learn python.  

5. still having problems mounting cluster and examining output **update RESOLVED. port 22 incoming is indeed blocked, but I can tunnel to the cluster on port 20400, like I used for mounting, and then use scp from my desktop to local host with the same effect as rsync. ** 

6. was also having massive problems plotting the resulting footprint profile to file using Anil's `plot_accessibility_profile.py` script. It took me a long time to decode it, but the file names are hardcoded in there and I had to play with the python parser to get it to let me use my own and the such. I succeeded, after much much trial and error, only to discover that the plotting script opens an X session despite simply writing all output to pdf, and Yosemite does not play well with that. Had to download install xquartz on yosemite. 

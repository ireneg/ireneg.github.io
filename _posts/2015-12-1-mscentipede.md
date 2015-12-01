msCentipede ran overnight, and have now called binding on a couple of PWMs. Some notes:

1. output is gzipped. I somehow missed that/it's not documented, so I will have to change file names in script.

2. chimps are far slower than humans - probably due to having more data. After 16 hours running not a single chimp pwm is done and none of the log likelihoods appears ready to converge. There's a lot of PWMs out there, so this might be a big problem...
    
    * maybe thin the chimps out so there's the same number of reads involved? the number of bound sites is the same, so either the data quality is worse or...

3. now looking for scripts to plot the results and check the footprint shape. 
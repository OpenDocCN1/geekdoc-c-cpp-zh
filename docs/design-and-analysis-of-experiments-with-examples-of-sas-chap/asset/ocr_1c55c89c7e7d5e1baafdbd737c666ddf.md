means are larger than the control means, change the means statement above to means treat/dunnett( 'A' ); This will give a one-sided lower confidence bound on the difference in means (experimental-control). If the lower bound is greater than zero, the experimental mean is significantly higher than the control mean. The same result can be obtained from the lsmeans by changing the command to lsmeans treat/diff=control('A') cl adjust=dunnett ; To get a one-sided test of whether the experimental means are less than the control, change dunnett to dunnettl in the means statement or controlu( 'A' ) to controlu( 'A' ) in the lsmeans statements.

When there is no control level of the treatment factor, there may still be interest in comparing all treatment levels to the best level. For example in an experiment to see the effect of the download site on the time to download a file, it may be of interest to find those sites whose download times are not significantly higher than the site with the minimum observed mean download time. To compare all treatment levels to the observed best level and to control the experimentwise error rate, the MCB procedure (Hsu, 1984) turns out to be equivalent to Dunnett's procedure. Look at the observed cell means in the data, determine which is the best, label the best as the control level, and use the dunnett option. For example, in the means for the experiment to compare download times for different download sites shown at the end of Section 2.8.2, site B had the shortest observed download time. To compare all other sites to B use the command:

```
proc glm;
class site;
model dtime=site;
means site/dunnett('B');
run;
```

Those sites that are not significantly different from B can be considered to be a subset of sites that have the fastest download times.
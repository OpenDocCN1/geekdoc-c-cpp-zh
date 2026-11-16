# Application: Replication of Marsh SDQ Data

This example demonstrates a replication analysis for EFA using Osborne & Fitzpatrick's (2012) procedure. We use internal replicability analysis with the SDQ data, randomly subsampling two independent samples from the original sample that are then analyzed separately using specific extraction and rotation guidelines based on our previous analyses of the scale. We are using the SDQ data because it is sufficiently large enough (N=15,661) to permit us to draw two moderately sized subsamples from the data. Unfortunately, the engineering and GDS data sets are not large enough to allow us to subsample from the data. If we were to do so, this would result in sample sizes of less than 240 and subject to item ratios of less than 13:1. If we remember the previous chapter, these are not ideal conditions for an EFA!

Before we get started, let's review the syntax to subsample from a data set. We use the SURVEYSELECT procedure, as we did for an example in the previous chapter. The code to produce our two subsamples is presented and described below.

```
*Sample 1;
proc surveysselect data = sdqdata method = SRS n = 500
out = sdqdata_s1 seed = 37;
run;

*Sample 2;
proc surveysselect data = sdqdata method = SRS n = 500
out = sdqdata_s2 seed = 62;
run;
```

In the code above, the DATA argument specifies the input data set to sample records from; the METHOD argument specifies the method of sampling (note that we use simple random sampling without replacement above); the N argument specifies the number of records to include in our subsample; the OUT argument specifies the name of the data set to contain the subsample; and the SEED option sets the seed to our random number so that we can rerun this code and get the same subsample.

After we draw out two subsamples from the original data, we conduct an EFA on each data set. We take care to apply the same methods (e.g., extraction, rotation) to each data set so that differences in the results are attributable to the data and not the methods. Consistent with our findings in previous chapters, we use maximum likelihood extraction and direct oblimin rotation. We also report a three-factor solution (the factor structure suggested by previous research on the scale) as well as two- and four-factor solutions to demonstrate how misspecification of a factor model can quickly become evident through replication analysis. An example of the basic syntax for the three-factor solution run on the first sample is presented below.

```
proc factor data = sdqdata_s1 nfactors = 3 method = ml
rotate = OBLIMIN fuzz=.3;
```

both analyses and (b) whether the individual item factor loadings are roughly equivalent in magnitude—the former being the basic threshold for successful replication, and the latter being a more reasonable, stronger definition of replication.

## A two-step procedure for comparing EFA solutions.

As noted above, we have not yet found a single summary statistic that meets our standards to evaluate EFA solution equivalency. In 2012 the first author and one of our graduate students conducted a review of replication procedures in EFA and developed two-step comparison procedure for evaluating EFA solutions (Osborne & Fitzpatrick, 2012).

First, Osborne & Fitzpatrick (2012) assess whether the basic factor structure is replicated. Regardless of whether the researcher is performing internal (a single sample, randomly split or external (two independently gathered samples) replication, the researcher needs to perform the same EFA procedure on both, specifying the same number of factors to be extracted, the same extraction and rotation procedures, etc. The researcher should then identify the strongest loading for each item (i.e., which factor does that item “load” on), and confirm that these are congruent across the two analyses. For example, if item #1 has the strongest loading on factor 1, and item #2 has the strongest loading on factor #2, that pattern should be evidenced in both analyses. If any items fail this test, we would consider these analyses to fail to meet the most basic threshold of replicability: structural replicability. There is therefore little reason to expect factor structure to replicate in any basic way in future samples.

If there is a small percentage of items that seem volatile in this way, this replication analysis might provide important information—that these items might need revision or deletion. Thus, replication can also serve important exploratory and developmental purposes. If a large number of problematic items are observed, this represents an opportunity for the researcher to revise the scale substantially before releasing it into the literature, where this volatility might be problematic.

Next, Osborne & Fitzpatrick (2012) evaluate whether the relative magnitude of the factor loadings is replicated. They advocate for simply subtracting the two standardized (rotated) factor loadings for congruent items, and squaring the difference. Squaring the difference has two benefits: eliminating non-important negative and positive values (if one loading is .75 and one is .70, subtracting the first from the second produces a -0.05, and subtracting the second from the first produces a 0.05, yet the direction of the difference is unimportant—only the magnitude is important) and highlighting larger differences. Researchers can then quickly scan the squared differences, and they can then either confirm that all are small and unimportant, or identify which items seem to have large differences across replication analyses.

As you might imagine, we find Osborne & Fitzpatrick’s procedure to be rather sensible. The procedure addresses both questions that we seek to address in a replication analysis: 1) Does the factor structure replicate? and 2) Are the factor loadings of similar magnitude?

## Application: Replication of Marsh SDQ Data

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
VAR Math: Par: Eng.;
run;
```

Three-factor replication analysis. An overview of the replication is presented in Table 6.1 on page 103. As you can see in this table, the two samples have identical factor structures. Even though the items that load on factor 2 in sample 1 are found to load on factor 3 in sample 2, these are still identical structural solutions because the same sets of items are loading on each factor. Thus, these two samples pass the first test of replicability—consistent factor structure. In addition, notice that the squared differences in factor loadings are all relatively small. The largest difference is .005, suggesting that the factor loadings do not differ by more than |.07|—which is not bad. We would suggest that after the squared differences achieve a magnitude of .04, indicating a difference of |.20|, a researcher can begin to consider factor loadings to be volatile. However, based on our current results, we can conclude that the two samples pass the second test as well—consistent magnitude of factor loadings.

### Table 6.1 Three-factor SDQ replicability analysis, ML extraction, oblimin rotation

| Variable | Sample 1 Comm | Sample 1 Factor 1 | Sample 1 Factor 2 | Sample 1 Factor 3 | Sample 2 Comm | Sample 2 Factor 1 | Sample 2 Factor 2 | Sample 2 Factor 3 | Squared Differences |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Eng1 | .61 | | .77 | | .69 | | .83 | | .0038 |
| Eng2 | .65 | | .82 | | .67 | | .84 | | .0006 |
| Eng3 | .75 | | .86 | | .68 | | .82 | | .0018 |
| Eng4 | .48 | | -.68 | | .49 | | -.66 | | .0006 |
| Math1 | .78 | .90 | | | .75 | .87 | | | .0010 |
| Math2 | .75 | .87 | | | .81 | .90 | | | .0007 |
| Math3 | .77 | .87 | | | .74 | .86 | | | .0002 |
| Math4 | .47 | -.65 | | | .38 | -.61 | | | .0019 |
| Par1 | .54 | | | .73 | .50 | | | .70 | .0008 |
| Par2 | .42 | | | -.67 | .49 | | | -.73 | .0033 |
| Par3 | .63 | | | .79 | .73 | | | .85 | .0041 |
| Par4 | .38 | | | -.53 | .36 | | | -.55 | .0002 |
| Par5 | .59 | | | .76 | .49 | | | .69 | .0045 |
| Eigen: | | 3.58 | 2.12 | 2.11 | | 3.49 | 2.45 | 1.85 | |

Note: Loadings less than 0.30 were suppressed to highlight pattern. Pattern coefficients were reported.

Although examination of communalities and eigenvalues is not part of our replication procedure, they can give us additional information about our samples and solutions. In the above table, the final extracted communalities for the items in each sample are very similar. If we were to take the difference between the two communalities, they would range between .01 and .10. This indicates approximately the same amount of unique variance is being extracted from each item in the two samples—a good sign for our replication analysis!

The final eigenvalues differ a little more because they are the sum of the partitioned item level variance. Remember, the unique variance that is associated with each item is then further divided among the factors. All of the tiny differences in the extracted variance are compounded in the eigenvalues, resulting in larger differences. Furthermore, the order in which the factors are extracted is determined by their eigenvalues. Thus, in sample 1 the factor that the parenting items load on is extracted third because it has the smallest (just barely) eigenvalue. However, in sample 2, the factor that these items load on is extracted second because it has a slightly larger eigenvalue. As we mentioned above, these differences in extraction order are not important when examining structural replication, but they do tell us that the relative weight of the factors has shifted slightly. In this example, the parenting items explain more variance in sample 2.

Finally, for fun, we made SAS do all the work in the analysis for us. We output our pattern matrix to a SAS data set and then merged and compared the two results. The syntax to do this, along with line comments for explanation, is presented below. Note, the syntax to create the two subsamples is provided above and is not included here.

```
*Conduct EFA Analyses;
*ODS output system used to output pattern matrix;
ods output ObliqueRotFactPat=SS1_pattern1;
proc factor data = sdqdata_s1 nfactors = 3 method = ml
rotate = OBLIMIN fuzz=.3;
VAR Math: Par: Eng:;
run;
ods output ObliqueRotFactPat=SS2_pattern1;
proc factor data = sdqdata_s2 nfactors = 3 method = ml
rotate = OBLIMIN fuzz=.3;
VAR Math: Par: Eng:;
run;
ods output close;
```

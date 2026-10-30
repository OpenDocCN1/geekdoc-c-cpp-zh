STEP 3. Compute the values of b0 and b1 in the model y = exp(b0 + b1 x) that minimize the deviation (6.5).

STEP 4. Interpret the results and the odds ratio.

We'll step through an example following the outline above.

# Example 6.10. Hospital Surgeries.

A group of hospitals has collected data on the numbers of Caesarean surgeries vs. the total number of births (see Table 6.11).

# TABLE 6.11: Total Births vs. Caesarean Surgeries

| Total | 3246 | 2750 | 2507 | 2371 | 1904 | 1501 | 1272 | 1080 | 1027 | 970 |
| Special | 26 | 24 | 21 | 21 | 21 | 20 | 19 | 18 | 18 | 17 |
| Total | 739 | 679 | 502 | 236 | 357 | 309 | 192 | 138 | 100 | 95 |
| Special | 17 | 16 | 16 | 16 | 16 | 15 | 14 | 14 | 13 | 13 |

Use the hospitals' data set to perform a Poisson regression following the steps listed above.

STEP 0. Enter the data.

```
> zhc := [3246,2750,2507,2371,1904,1501,1272,1080,1027,970,739,679,502,236,357,309,192,138,100,95] :
> yhc := [26,24,21,21,21,20,19,18,18,17,17,16,16,16,16,15,14,14,13,13] :
> N := nops(yhc);
N := 20
```

STEP 1. Plot a histogram, and then perform a Chi-square Goodness-of-fit test on yhc, if appropriate.

(Note: Maple's Histogram function is in the Statistics package. There are a large number of options for binning the data; we will use frequencyscale = absolute to have the heights of the bars equal to the frequency of entries in the associated bin. Collect the bin counts with TallyInto.)

```
> with(Statistics):
Dirac(0) := 1.0: # needed for the Poisson distribution
> Bins := $[min(yhc)..max(yhc)];
Bins := [13,14,15,16,17,18,19,20,21,22,23,24,25,26]
```
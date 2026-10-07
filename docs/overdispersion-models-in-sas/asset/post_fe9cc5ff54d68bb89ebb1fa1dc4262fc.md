
# Program 4.2: Goodness-of-fit Tests—Chromosome Data

| title |
|------------------------------------------------------------|
| This Macro performs a Pearson's GOF Test |
| Skellam's (1948) Chromosome Data Example |
| data = data set containing the variables Obs and Pred |
| df = degree of freedom |
| title = Distribution being fit |

```sas
%macro gof(data,df,title);
proc imml;
  use &data;
  read all(freq) into Observed;
  read all(Pred) into Predicted;

  gof = sum(Observed # Predicted) - &n;
  pvalue = 1 - probchi(gof,df,0);

  Summary = j(3,1,0);
  Summary[1,1] = gof;
  Summary[2,1] = &df;
  Summary[3,1] = pvalue;

  label = { 'Pearson's GOF Test',
  'Degrees of Freedom',
  't-value'};
  print &title;
  print Observed Predicted[format=10.4];
  print Summary[label=rowname format=10.4];
quit;
%mend gof;

ods html;
%gof(pred1,1,'Binomial Distribution');
%gof(pred2,1,'Beta-binomial Distribution');
%gof(pred3,1,'Random-connected Binomial Distribution');
%gof(pred4,1,'Zero-correlated Binomial Distribution');
%gof(pred5,1,'Generalized-Binomial Distribution -- Additive Interaction');
ods html close;
```

Output 4.2 shows the GOF results only for the Beta-binomial distribution.

# Chapter 4 Likelihood Models for Overdispersed Binomial Responses 93

Output 4.2: GOF Results under the Beta-binomial Distribution

| Beta-binomial Distribution |
| Observed | Predicted |
| 32 | 33.9692 |
| 103 | 97.1628 |
| 122 | 127.6667 |
| 80 | 78.2014 |

| Summary |
| Pearson's GOF Test | 0.7577 |
| Degrees of Freedom | 1.0000 |
| P-value | 0.3840 |

Table 4.3 shows the observed and expected frequencies of the number of associations under the five distributions considered in this example. The Binomial distribution does not fit the data well, since $X^2 = 8.11$ on two degrees of freedom with an associated P-value of 0.017. A similar observation can be made about the Zero-inflated Binomial, where $X^2 = 4.71$ on one degree of freedom with an associated P-value of 0.030. Degrees of freedom are computed as (number of categories minus minus) (number of parameters estimated). In the case of the Binomial distribution, degrees of freedom are $(4-1)=2$. The overdispersed distributions have an additional parameter, $\rho$. That makes their degrees of freedom $(4-1)-2=1$. The Binomial, the Random-clumped Binomial and the Generalized-Binomial with Additive Interaction fit the distribution of the number of associations fairly well, with P-values of the Chi-squared GOF tests being 0.384, 0.347 and 0.439, respectively. When there are multiple models, all are acceptable by a Goodness-of-fit criterion, and the models are not nested within each other, is difficult to choose a single model as the final recommendation. This can happen even in a regression modeling situation. Consequently, it is advisable to discuss the options with the subject-matter experts and communicate to them the meaning of each model and seek their input as which model is closer to the phenomenon they study.

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

# Table 4.3: Pearson's Chi-square Goodness-of-fit Tests for Chromosome Data

| Number of Associations | Observed Frequency | Binomial | Beta-binomial | Random-clumped Binomial | Zero-inflated Binomial | Generalized-Binomial |
|---|---|---|---|---|---|---|
| 0 | 32 | 24.86 | 33.97 | 34.08 | 32.00 | 33.91 |
| 1 | 103 | 103.24 | 97.16 | 96.82 | 93.60 | 97.55 |
| 2 | 122 | 142.94 | 127.67 | 128.24 | 140.80 | 126.84 |
| 3 | 80 | 65.96 | 78.20 | 77.85 | 70.60 | 78.70 |
| $\chi^2$ | | 8.11 | 1 | 1 | | 1 |
| P-value | | 0.017 | 0.384 | 0.347 | 0.030 | 0.439 |

## Pearson's Chi-square Goodness-of-fit Tests for Chromosome Data

As we have seen earlier, the Beta-binomial and Random-clumped distributions, for cluster size m, are nearly identical. Note that as $\rho$ approaches unit, the differences between them become pronounced.

[Note: The OCR text contained significant repetitive and garbled sections which have been cleaned up based on logical flow.]

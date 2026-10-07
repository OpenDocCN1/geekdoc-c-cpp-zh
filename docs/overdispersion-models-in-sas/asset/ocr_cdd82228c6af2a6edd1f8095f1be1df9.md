# Chapter 6 Likelihood Models for Overdispersed Count Responses 167

# 6.4 Example of Number of Eggs of the Intestinal Trematode Schistosoma Mansoni

Trematodes are a class of flatworms which includes both external and internal parasites of animal hosts that have a thick outer cuticle and one or more suckers or hooks for attaching to tissue. They are also called fluke. Among the trematodes Schistosoma Mansoni causes a disease known as Schistosomiasis (also known as bilhariasis or snail fever). This disease is most commonly found in Asia, Africa, and South America, especially in areas where the water contains freshwater waters which may carry the parasite. Cohen (1966) analyzed a sample counts of the number of eggs of the intestinal trematode Schistosoma Mansoni, on single slides, collected from 926 inhabitants of an Egyptian village. The population sampled consists of a mixture of an infected group with a non-infected group.

Table 6.1: Trematode Schistosoma Mansoni Counts

We will fit the Negative-binomial (NB) and the Zero-inflated Negative-binomial (ZINB) models to the trematode Schistosoma Mansoni counts of Table 6.1, and compute the traditional Pearson's Goodness-of-fit Chi-square statistic

> $$\chi^2 = \sum_{k=0}^{c} \frac{(O_k - E_k)^2}{E_k}$

$O_i$ and $E_i$, respectively, the observed and expected counts, and where $c$ represents the number of categories. As we collapse the counts of 8 or 9 eggs into one category, and the 10 or more into another category. Thus, the number of categories will be $c=10$. We will make use of the COUNTREG procedure in order to get the maximum likelihood estimates under both the NB and the ZINB. COUNTREG assumes the logarithm link on the parameter $\mu$ and identity link on the dispersion parameter $\kappa$ ; it allows the user to select either a log or alogit link on the parameter $\omega$. We output from each fitted model the estimates of $Prob(Y=y)$, $y=0,1,...,14$. The observed and expected counts are computed using the MEAN. The final computations of the Pearson's Goodness-of-fit

Morel, J. and Nagaraj Neerchal. Overdispersion Models in SAS.. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.
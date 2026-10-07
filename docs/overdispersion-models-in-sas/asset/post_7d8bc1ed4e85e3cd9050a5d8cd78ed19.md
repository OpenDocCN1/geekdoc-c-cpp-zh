
# Preface

happily celebrating 20 years of continuous research collaboration on the topic of dispersion.
This book is an apt celebration of these 20 years!

Preparing the material for this book was greatly facilitated by a number of short courses taught in 2003 and 2004. We list them below to acknowledge the respective sponsors.

- “Modeling and Analysis of Categorical Data with Overdispersion”. Sponsored by the Biopharmaceutical Section of ASA. 2004 Joint Statistical Meetings, Toronto, Canada. August 10, 2004.
- “Analysis of Categorical Data with Overdispersion”. By invitation of Dr. Gregory Campbell, Director of Biostatistics, Office of Surveillance and Biometrics, Federal and Drug Administration (FDA), Rockville, Maryland. March 12, 2004.
- “Analysis of Categorical Data with Overdispersion”. 54th Session International Statistical Meeting, Berlin, Germany. August 12, 2003.
- “Analysis of Categorical Data with Overdispersion”. Midwest Biopharmaceutical Workshop, Munich, Indiana. May 19, 2003.

In this book, we present examples from a variety of application areas rather than focusing on a single area, we believe, because of the high quality of overdispersion, as well as versatility of the methods presented here. Towards that end, there are 30 sets discussed throughout this book. Some examples are: toxoplasmosis in sampled subjects in 33 cities of El Salvador, ossification of the phalanges on rats to environmental agents, forest pollen columns, chromosomal aberrations in the atomic bomb explosion in Hiroshima, Sikel's and Ebert's memory, urinary tract infections in HIV, hospitalization in significant neighborhoods, seizure counts for epilepsy, shoulder pain after surgery, etc.

The authors are indebted to many people whose assistance led to the completion of this book. We thank Dr. Santos C. Sutherland from Pfizer, Inc., and Dr. Jan Newell from Sandia National Laboratories, for allowing us to use their SAS in this book. Prof. Dirk F. Moore from the Department of Biostatistics, University of Medicine and New Jersey, provided us the Hiroshima chromosome aberration data discussed in Chapter 5. Prof. Jan den Broek from the Center of Biostatistics, Utrecht of the Netherlands, provided the urinary tract infection in men with HIV discussed in Chapter 6.

We thank Dr. Oliver Schaberberger for SAS Institute for an encouraging conversation at the 2008 Statistical Meetings in Denver, Colorado, which gave us the momentum to undertake the task of writing this book. The incorporation of some of our work into PROC GLIMM (EMPIRICAL-MBN) and into PROC SURVELOGISTIC (VARAF-MOREL) is a highlight of our path down the dispersion lane! SAS (anonymous to us) have provided numerous comments and suggestions that resulted in improvement in the presentation. We also thank SAS administrators Shelley Sessions who initiated this project. We also thank Dr. Greg Gray, Callie Jender, and Dan Schneider of Procter & Gamble for providing the facility and facilitating the internal clearance process, and Dr. Robert Bartlett and vice-president Dr. Nora Zorich for their support. A. Paige Rogers, Director of the Writing in the Disciplines and the Curriculum Program at the Community College of Baltimore County, provided multiple editorial reviews of the manuscript. We also thank Dr. DoHwan Park and her students in the special topics course on Generalized Linear Models (Fall 2011 at UMBC) for providing reviews of the penultimate draft. While we thank all our reviewers, we take full responsibility for all remaining blemishes.

# Preface

We have been very fortunate to have worked with a number of graduate students at the Department of Mathematics and Statistics, University of Maryland Baltimore County (UMBC) on Overdispersion: Santos and Justin, mentioned earlier, and Drs. Minglei Liu and Maxime Bokossa. We thank them for their intellectual companionship. Furthermore, we gratefully acknowledge our colleagues at Proctor & Gamble and UMBC for the stimulating environment conducive to good work.

Finally, a debt of gratitude is due to our families (Jorge: Grecia and David; Nagaraj: Chetana, Harsha, and Siri). Their patience, which allowed us numerous escapes from daily chores, made this book possible. Thank you!

Morel, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

Morel, Jorge, and Nagaraj Neerchalk. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.

# Overdispersion

- 1.1 A Simple Introductory Example..................................................................................6
- 1.2 Overdispersion...............................................................................................................3
- 1.3 A Common Characterization of Overdispersion...............................................................4
- 1.4 An Extended Definition of Overdispersion......................................................................6
- 1.5 A Simulated Example......................................................................................................7
- 1.6 The Exponential Family...............................................................................................11
- Appendix 1.1: Hierarchical Models to be Covered in this Book ................................14

# 1.1 A Simple Introductory phenytoin

The anticonvulsant is known to be teratogenic on the prenatal development of inbred mice. Hartfields et al. (1990) conducted a completely randomized experiment with 81 pregnant mice to investigate the potential synergistic effect of phenytoin (PHT) and trichloropropene oxide (TCPO). The study was set up as 2x2 factorial: PHT and TCPO were administered at 0 mg/kg, 60 mg/kg, and 100 mg/kg. The presence or absence of ossification in the middle phalanges is a measure of the teratogenic effect. In some phalanges the ossification did not occur; in others, it was almost complete. To simplify this part of our study, we analyzed only the left paw. Table 1.1 depicts the number of fetuses showing ossification in the middle third. This example is used here in a simple form to introduce the concept of overdispersion and will be revisited in greater depth.

![](img/fa9648c17451eb7d92f5fb_13_0)

# # Overdispersion Models in SAS

Table 1.1: Ossification Data for 11 Mice Exposed to Phenytoin (PHT) and Trichloropropene Oxide (TCPO)

| Mouse (j) | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | Total |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Number of fetuses showing ossification ($t_j$) | 2 | 0 | 1 | 7 | 0 | 0 | 0 | 6 | 1 | | 18 |
| Total number of fetuses ($m_j$) | 2 | 7 | 8 | 10 | 4 | 6 | 7 | 6 | 7 | | 71 |

If $t_j$ and $m_j$, represent, the number of fetuses showing ossification and the total number of fetuses of the j-th mouse, $j=1,2,...,11$, the estimated probability of ossification in any middle third of the forearm can be calculated as

$$\hat{\pi} = \frac{\sum_{j=1}^{11} t_j}{\sum_{j=1}^{11} m_j}$$

which, in this example, turns out to be $18/71=0.2535$. If the $t_j$'s were truly distributed as Binomial random variables with parameters $(\pi, m_j)$, where $\pi$ is the underlying true probability of ossification, the estimator of the variance of $\hat{\pi}$, given that mice indicate, unbiased

$$\hat{Var}(\hat{\pi}) = \frac{\hat{\pi}(1-\hat{\pi})}{\sum_{j=1}^{11} m_j}$$

The value of this estimated variance is 0.027. Note that the above estimator is not valid if the Binomial model does not hold. Based on sampling theory (see Cochran 1977, p. 155), a consistent estimator, which does not depend on the binomial assumption, is

$$\bar{Var}(\hat{\pi}) = \frac{n\sum_{j=1}^{n}(t_j-m_j\hat{\pi})^2}{\sum_{j=1}^{n} m_j^2}$$

which turns out to be 0.0142. The remarkable difference between the model-based and sampling-theory estimate leads us to the following: Are these data really binomially distributed with a common probability of success $\pi$? An easy way to answer this question is by computing the Pearson's Chi-square

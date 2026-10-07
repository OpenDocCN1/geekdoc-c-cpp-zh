# Chapter 9 Generalized Estimating Equations Techniques for Marginal Models 329

express the probability of "Low" as a linear combination of the other two probabilities in order to be consistent with the Generalized Logit model used later, where this category will be used as the reference. Then, the homogeneity hypothesis (9.30) can be stated as

$H_0 : \pi_{12} = \pi_{22} \text{ Vs } \pi_{13} = \pi_{23} \text{ Vs } H_1 : \pi_{12} \neq \pi_{22} \text{ Vs } \pi_{13} \neq \pi_{23} ,$

or equivalently

$H_0 : \ln\frac{\pi_{12}}{\pi_{22}} = 0 \text{ Vs } \ln\frac{\pi_{13}}{\pi_{23}} = 0 \text{ Vs } H_1 : \ln\frac{\pi_{12}}{\pi_{22}} \neq 0 \text{ Vs } \ln\frac{\pi_{13}}{\pi_{23}} \neq 0 . (9.31)$

Note that the above represents the restatement of the homogeneity under a Generalized Logit link with the category "Low" as the reference category. In practice, if the hypothesis is raised, it is customary to consider two additional hypotheses, namely,

$H_0 : \pi_{12} = \pi_{22} \text{ Vs } H_1 : \pi_{12} \neq \pi_{22} (9.32)$

and

$H_0 : \pi_{13} = \pi_{23} \text{ Vs } H_1 : \pi_{13} \neq \pi_{23} (9.33)$

These hypotheses may be restated in terms of log-odds-ratio as follows

$H_0 : \ln\frac{\pi_{12}}{\pi_{22}} \neq 0 \text{ Vs } H_1 : \ln\frac{\pi_{12}}{\pi_{22}} \neq 0 (9.34)$

and

$H_0 : \ln\frac{\pi_{13}}{\pi_{23}} = 0 \text{ Vs } H_1 : \ln\frac{\pi_{13}}{\pi_{23}} \neq 0 . (9.35)$

$I(\cdot)$ represent a test-product indicator function, $i=1, 2$. Assuming the Generalized Logit link function

$$\ln\frac{\pi_{2i}}{\pi_{ii}} = \beta_0 + \beta_{1i}I(i=1)$$\n$\ln\frac{\pi_{3i}}{\pi_{31}} = \beta_{20} + \beta_{2i}I(i=1) (9.36)$

It follows that $\beta_1 = \ln\frac{\pi_{12}}{\pi_{22}} \text{ and } \beta_2 = \ln\frac{\pi_{13}}{\pi_{23}}, \text{ so the testing of hypothesis (9.31) boils down to testing simultaneously

$H_0 : (\beta_1, \beta_2) = (0,0) \text{ Vs } H_1 : (\beta_1, \beta_2) \neq (0,0)$

Morel, Jorge, and Nagaraj Neeraj. Overdispersion Models in SAS.. Copyright 2011, SAS Institute Inc., Cary, North Carolina, USA: ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.
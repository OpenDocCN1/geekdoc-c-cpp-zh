# Overdispersion Models in SAS

| Exposure Factor | Yes | No |
| --- | --- | --- |
| Present | $\pi_{11}$ | $\pi_{12}$ |
| | $\pi_{+1}$ | $\pi_{+2}$ |
| Absent | $\pi_{21}$ | $\pi_{22}$ |
| | $\pi_{+1}$ | $\pi_{+2}$ |
| Total | 1 | 1 |

It is impossible to reconstruct the probabilities under a prospective study from the information given above. However, all is not lost because the OR can be recovered from the information given above. The odds-ratio is now defined as the ratio of the odds of having the exposure factor when the disease is present and the odds of having the exposure factor when the disease is absent. These odds are defined as

> Odds(Having the Exposure Factor when the disease is Present) = $\frac{\pi_{11}}{\pi_{+1}} = \frac{\pi_{11}}{\pi_{21}}$

and

> Odds(Having the Exposure Factor when the disease is Absent) = $\frac{\pi_{12}}{\pi_{+2}} = \frac{\pi_{12}}{\pi_{22}}$

Thus, for a case-control study the odds-ratio is

> OR = Odds(Having the Exposure Factor when the disease is Present) = $\frac{\pi_{11}}{\pi_{+1}} = \frac{\pi_{11}}{\pi_{21}}$
Odds(Having the Exposure Factor when the disease is Absent) = $\frac{\pi_{12}}{\pi_{+2}} = \frac{\pi_{12}}{\pi_{22}}$

Note that the odds-ratio is the same both prospective and case-control (retrospective) studies. It is said that the odds-ratios are "invariant to the sampling scheme." This fact becomes important for epidemiologists, medical researchers and public health practitioners in case-control studies. In such studies, it turns out that the Relative Risk, RR = $\frac{\pi(X=1)}{\pi(X=0)}$

cannot be directly obtained. On the other hand, computing odds-ratio is straightforward. Under these circumstances, it is well known that the odds-ratio and the relative risk are practically the same (Cornfield, 1951). These two properties of the odds-ratio, invariance to the nature of the study and almost identical value to the relative risk, logistic regression make one of the most appealing statistical regressions

More, Jorge, and Nagaraj Neerchal. Overdispersion Models in SAS®. Copyright © 2011, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED. For additional SAS resources, visit support.sas.com/publishing.
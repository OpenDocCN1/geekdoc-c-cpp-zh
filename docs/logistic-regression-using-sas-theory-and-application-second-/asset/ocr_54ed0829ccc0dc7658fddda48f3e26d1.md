multiple points in time, we ordinarily expect those observations to be positively correlated.
But there are many other applications in which the data have a cluster structure. For example, husbands and wives are clustered in families, and students are clustered in classrooms. In studies involving matching, each match group is a cluster. And, of course, cluster sampling naturally produces clustered observations.

There are several reasons why logistic regression should take clustering into account:

+   - Ignoring the clustering and treating the observations as though they are independent usually produces standard errors that are underestimated and test statistics that are overestimated. All methods for dealing with clustered data are designed to correct this problem.
+   - Conventional logistic regression applied to clustered data produces coefficient estimates that are not efficient. That means that there are, in principle, other methods whose coefficients have smaller true standard errors.
+   - In addition to these problems, clustered data also presents opportunities to correct for biases that may occur with any application of binary regression. One method for clustered data can correct for heterogeneity shrinkage. Another method can correct for bias due to omitted explanatory variables.

In this chapter, I’ll discuss five different methods for clustered data that can be implemented in SAS:

+   - Robust standard errors with PROC GENMOD and PROC SURVEYLOGISTIC
+   - Generalized estimating equations (GEE) with PROC GENMOD
+   - Conditional logit (fixed-effects) models with PROC LOGISTIC
+   - Mixed models (random effects) with PROC GLIMMIX
+   - A hybrid method that combines fixed-effects with mixed models

# 8.2  Longitudinal Example

Let’s begin with an example of longitudinal data, also known as panel data. The sample consisted of 316 people who survived residential fires in the Philadelphia area (Keane et al. 1996). They were interviewed at 3 months, 6 months, and 12 months after the fire. For each interview, the outcome variable PTSD is coded 1 if the person had symptoms of post-traumatic stress disorder, and 0 otherwise. The explanatory variables measured at each interview are
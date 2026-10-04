# Applied Time Series Analysis with R

as daily stock prices. However, the explosive realization associated with
$\phi_1=1.1$ is not similar to that of any data sets that we will attempt to
analyze, being better modeled as a deterministic process.

# EXAMPLE 3.4: STOCK MARKET DATA

In Figure 3.8 show daily Jones closing averages for 2014 (data
dowjones2014 in tswge). (Source: Federal Reserve Bank.) It can be
seen that the series have the typical wandering appearance of an
AR(1) process with positive $\phi_1$. The sample autocorrelations and Parzen
spectral estimate are shown in Figure 3.8b and c where it can be seen that
tautocorrelations are slowly exponentially decaying, and the spec-
density has a peak at zero. By comparing Figure 3.8 with Figures
3.4 through 3.6 it can be seen that $\phi_1$ appears to be close to one, that is,
near nonstationary. We will return to the analysis of data such as in
Figure 3.8 when we discuss the topics of nonstationarity, model identifi-
cation, and parameter estimation.

# 3.2.3 AR(p) Model for $p \ge 1$

Now that we have discussed the properties of the simplest of all AR mod-
els, the AR(1), we turn our attention to the more general case in which $p \ge 1$.

![](bbox=[0.276, 0.502, 0.676, 0.676])

![](bbox=[0.136, 0.699, 0.852, 0.875])

**FIGURE 3.8**n(a) Jones daily closing averages for 2014, (b) sample autocorrelations, and (c) Parzen
spectral density estimate.
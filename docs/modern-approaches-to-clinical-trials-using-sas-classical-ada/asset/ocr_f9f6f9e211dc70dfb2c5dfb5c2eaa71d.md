# 7.5.3 Example 2: neurodeg Data for Generalized MCP-Mod Approach with Model Averaging

The second example concerns regards simulated data from [4] to illustrate the use of the generalized MCP-Mod approach. The data set is available under the name neurodeg from the DoseFinding R package. The SAS code used for the computations and summarization of all results can be found in Appendix D.

This example refers to a phase II clinical study for a neurodegenerative disease. The disease status is measured through a functional scale, with smaller values corresponding to more severe neurodegeneration. The goal of the drug is to reduce the rate of disease progression, which is measured by the linear slope of the functional scale over time.

The trial design includes a placebo and four doses: 1, 3, 10, and 30 mg, with balanced allocation of 50 patients per arm. Patients are followed up for one year, with measurements of the functional scale being taken at baseline and every three months thereafter. The study goals are to (i) test for a dose-response signal, (ii) estimate the dose-response, and (iii) select a dose to be brought into the confirmatory stage of the development program.

The functional scale response is assumed to be normally distributed and, based on historical data, it is believed that the longitudinal progression of the functional scale over the one year of follow up can be modeled by a single linear trend. A mixed model is assumed for the functional scale for the measurement $y_{ij}$ of patient $i$ at time $j$,

```
$y_{ij} = (eta_0 + b_{0j}) + (\mu(x) + b_{v})x_{ij} + \epsilon_{ij}, [b_{0j}\sim N(0,\Omega)$ and $\epsilon_{ij}\sim N(0,\sigma^2)$.
```

Consequently, the dose-response parameter of interest in this situation is the slope of disease progression associated with the dose $d$. Assume that the candidate models for $\mu(x)$ in this example include a model with $ED_{50} = 1.11$, an exponential model with maximum effect $\delta = -0.022$, and a linear model $\delta=8.867$. Fitting the mixed model above using the proc glmix call in Example Code
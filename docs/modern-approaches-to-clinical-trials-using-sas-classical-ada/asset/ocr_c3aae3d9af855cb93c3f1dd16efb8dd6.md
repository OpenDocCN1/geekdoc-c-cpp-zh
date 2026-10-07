0 62 0.011 0.38

1 74 0.091 0.36

3 69 0.093 0.35

9 70 0.122 0.34

27 67 0.215 0.35

81 67 0.246 0.39

# Example Code 8.2 Analysis of Asthma Trial with 75 Patients Per Group

```
/** MCMC syntax sets the data set to output posterior summaries, sets
number of monte carlo iterations along with the seed, parameters to monitor,
plots to monitor autocorrelation and thinning **/
proc mcmc data = outemaxsim nmc = 50000 nbi = 1000 seed = 3746
monitor = (parme, var_sub, std_sub) ed50 len50)
thin = 9 stats (percenter.5 15 50 75 95 97.5);
ods outputPostsummariespostIntervals-intervals;
param e0 max len50) /** set parameters **/
/** Setting prior for each parameter **/
prior e0-normal(mean=0, precision=10)
prior emax-normal(mean=0.20, precision=10)
prior tau-gamma(shape=0.001, scale=0.001)
prior len50-normal(mean=-0.69, precision=0)
beginprior
  /** Setting residual variance ***/
  var_sub = 1/tau;
  std_sub = sqrt(var_sub);
  /** Ed50 ***/
ed50 = exp(len50);
  /** Calculating the posterior predictive distribution ***/
Preddist output=predout nsmim=5000 covariates=Sumstat;
enddata;
mu = e0 + (emax/dose)/(ed50 + dose);
model response - normal(mean=mu, precision=tau);
run;
```

The proc mcmc statement uses the input data set sims (data = ) that we have generated using the macro Example Code 8.1 Simulated Data for Asthma Trial with 75 Patients Per Group. The posterior samples will be saved in the emax_out data set using the outpost option. In this example, 50,000 markov chain simulations (nmc) are planned with 1,000 burn-in samples (obi) and a thinning rate of 3 (thin), implying that every 3rd simulation sample is kept with the remaining samples discarded. The model parameters and all initial values are specified in the prior specified in the prior statement, the priors are specified in the prior
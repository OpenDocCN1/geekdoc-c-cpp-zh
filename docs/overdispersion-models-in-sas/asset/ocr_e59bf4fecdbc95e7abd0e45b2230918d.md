Chapter 8 A Two-stage Maximum Likelihood Estimation Procedure 269

*** Fisher Scoring Method using approximate RCM -- Random-clumped Multinomial Distribution ***

NOTE: Convergence criterion (EPSILON=1E-8) satisfied

Maximum Likelihood Estimates using FIM and Approximate Fi -- Random-clumped Multinomial Distribution

| Parameter | Estimate | StdErr | AppStdErr | Pct_Rel_Error |
| --- | --- | --- | --- | --- |
| Pi(1) | 0.50366 | 0.068912 | 0.068911 | 0.00076 |
| Pi(2) | 0.43163 | 0.068150 | 0.068150 | 0.00086 |
| Rho | 0.43154 | 0.104128 | 0.104129 | 0.00124 |
| Log Likelihood | -43.38522 | | | |

# Appendix 8.1: Simulation Results

In this Appendix, we report the results of a simulation study conducted by Neerhal and Morel (2005) on the performance of the Two-stage method proposed in Section 8.3. The simulation study consisted of 5,000 data sets, each of sample size n=250. combinations of parameter values and cluster sizes (m) were considered. For each model, two sets of maximum likelihood estimates were computed, starting from the initial values. One was computed using the exact FIM (8.2). The other set was computed using the approximations given by equations (8.3) and (8.4). Then, an overall relative error of the approximate likelihood estimates with respect to the exact maximum likelihood estimates was computed. More specifically, with titles corresponding to the estimates obtained using the approximate FIM and hats corresponding to the exact maximum likelihood estimates, we have

Monte Carlo Error ($\tilde{\pi}$) = Maximum 5,000 Replications of $\frac{\sqrt{\frac{1}{d}\sum_{i=1}^{d}|\hat{\pi}_i - 	ilde{\pi}|^2}}{	ilde{\pi}}$

Monte Carlo Error ($\tilde{ho}$) = Maximum 5,000 Replications of $\frac{\sqrt{\frac{1}{d}\sum_{i=1}^{d}|\hat{ho}_i - 	ilde{ho}|^2}}{	ilde{ho}}$

Monte Carlo Error {$\tilde{\sigma}$} = Maximum 5,000 Replications of $\frac{\sqrt{\frac{1}{d}\sum_{i=1}^{d}|SE(\hat{\sigma}_i) - SE(\tilde{\sigma})|^2}}{SE(\tilde{\sigma})}$

and
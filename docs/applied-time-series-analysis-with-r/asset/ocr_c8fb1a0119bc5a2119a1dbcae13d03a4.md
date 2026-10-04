# Long-Memory Processes 493

+   4. sn=0 (default) produces results based on a randomly selected seed. If you want to reproduce the same realization on subsequent runs of gen.arma.wge then set sn to the same positive integer value on each run.

Example: The x=gen.arma.wge(n=30,u=0.8,lambda=0.35,phi=.8) generates and plots a realization from the model (1-0.8B) (1-2(0.8B+B^2))X, a=a, and stores it in the vector xss$data. The white noise was normally distributed with mean zero and since defaults were used, there are no MA parameters, the white noise variance is 1, a random seed is used, and the realization will be plotted.

+   d est.farma.wge(x,low.d,high.d,inc.d,p.max,nback) is a function that obtains estimates of a FARMA(p,d,q) model (with q=0) using the grid-search algorithm described in Section 11.5.

low.d is the vector of lower boundaries of d's in the grid search
high.d is the vector of upper boundaries of d's in the grid search
inc.d is the increment for d's in the grid search
p.max is the maximum AR order
nback is the number of backcast observations (see discussion following Equation 11.27

The program outputs:
d (the estimate of d)
phi (the estimates of the parameters $\phi_v,...,\phi_p$)
vara (The estimated white noise variance (based on backcast residuals))
ai associated with the final FARMA fit

NOTES:

+   1. We assume q=0, that is, there are no MA factors in the model.
2. For other CRAN functions that perform FARMA model identification, see Example 11.9(1).

Example: We use est.farma.wge to implement the grid-search procedure to estimate the parameters of the FARMA model fit to the Nile data in Example 11.9. The statement

test = est.farma.wge(Nile,low.d=0,high.d=0.5,inc.d=.001,p.max=3)
performs the calculations using the grid described in Example 11.9(1) and obtains $\hat{d}=0.37$ and $p=0$ as discussed in Example 11.9(1). Also
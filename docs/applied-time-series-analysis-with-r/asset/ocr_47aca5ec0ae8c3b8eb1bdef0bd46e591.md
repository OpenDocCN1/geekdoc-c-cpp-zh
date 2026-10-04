g. is.sample.wge(data,lambda,offset,phi) computes and plots
the instantaneous spectrum based on a spectral estimate of the dual
using a Parzen window.

lambda is the value of λ in the G(λ; p) model (default lambda = 0,
i.e. an M-stationary model)

offset is the offset parameter (see for example the discussion about
Figure 13.2 (default = 60)

Example: To compute the instantaneous spectrum based on a peri-
odog fit to the dual data in Figure 13.4b obtained from the data
in Figure 13.2c (and Figure 13.4a), using the following commands:

```
data(fig13.2)
is.sample.wge(fig13.2c, lambda = -0.4, offset = 63)
```

Compare with the AR-based instantaneous spectrum shown in
Figure 13.8c.

# 13B1 Filtering Steps Producing Figure 13.19e and f

```
data(fig13.18a)
#we will use true values (lambda = 0 and offset = 175)
dual=trans.to.dual.wge(fig13.18a, lambda = 0, offset = 175)
plot=FALSE
11=butterworth.wge(dual$intY, order = 4, type = 'low', cutoff = .05)
12=butterworth.wge(dual$intY, order = 4, type = 'low', cutoff = .05)
```

# EXERCISES

13.1 Using twsg function gen.lambda.wge create a realization of
length n = 256 from the Euler(4) model

```
X(h^k)-1.75X(h^{k-1})+1.95X(h^{k-2})-1.70X(h^{k-3})+0.95(h^{k-4})=a(h^k),
```

with offset 60.

+   a. What system frequencies should the dual data contain?

+   b. Fit an Euler model to the generated data by using function
est.lambda.wge and specifying λ = 0. Choose 0:200 as the off-
set range and 12 as the maximum AR order. 

+   c. Using the output printed by the program, show and discuss
plots of

+   i. The data

+   ii. The dual
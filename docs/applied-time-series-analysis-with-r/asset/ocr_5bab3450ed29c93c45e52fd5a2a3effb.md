vara is the white noise variance (default = 1)
plot = TRUE (default) produces a plot of the realization generated
sn determines the seed used in the simulation. (see Note (5) below).

# NOTES:

+   1. This function finds p as length of phi. If phi = 0 (default) the
value for p is set to zero.
2. gen.lambda.wge calls the tswge function gen.arma.wge
which in turn calls the base R function arma.sim.
3. It will be useful to call the utility mult.wge if you know
tactors of the AR model instead of coefficients.
4. By default the white noise is zero mean, normal noise with vari-
ance vara = 1
5. sn = 0 (default) produces results based on a randomly selected
runs if you want to produce the same realization on sub-
quent of gen.lambda.wge then set sn to the same posi-
t value on each run.

Example: The command

```
x = gen.lambda.wge(n = 500,lambda = 0.5,phi = c(1.9,-
.99),offset = 25, vara = 1)
```

generates and plots a realization from the model used to generate
t realization in Figure 13.6b. The seed is randomly selected,
realization generated here will not match Figure 13.6b exactly,
but it will have the decreasing frequency TV characteristics.

+   b. est.lambda.wge(x,lambda.range,offset.range) estimates
lambda and offset (within specified ranges) that produce the "most
stary") dual.

x is an exactly spaced TFV data set
lambda.range is a 2-component vector specifying the lowest and
hig values of lambda to be considered.

offset.range is a 2-component vector specifying the lowest and
hig values of offset to be considered.

Example: The commands to find the values of lambda and offset that create
the data set in Figure 13.4b are

```
data(fig13.2c
est.lambda.wge(fig13.2c,lambda.range = c(-.5,.5),offset
range = c(0,100))
```

NOTE: The top values of lambda and offset that were returned are
lambda = -0.4 and offset = 63. Example 13.7.
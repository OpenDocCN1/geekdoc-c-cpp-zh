alpha_1 = c\pi_1, and $\alpha_2 = c(1-\pi_1)$, then $p_1 = x_1$. Then generate $x_2$ from a Beta
distribution with parameter $\alpha_1 = c\pi_1$, and $\alpha_2 = c(1-\pi_1-\pi_2)$, and compute $p_2$

$p_2 = x_2(1-p_1)$. The d-th component of each Dirichlet distribution is obtained as

```
p_d = x_d \sum_{i=1}^{d} p_i, where x_d is generated from a beta distribution with parameters $\alpha_i = c\pi_d$
```

and $\alpha_2 = c(1-\sum_{i=1}^{d} \pi_i)$. Recall that $p_{d+1} = 1-\sum_{i=1}^{d} p_i$, so there is no need to generate the (d+1)

component. The RANDDIRICHLET function in the IML model library is used to generate a
random sample from a Dirichlet distribution.

Generation of data under the Random-clamped Multinomial model is much simpler and be
found in Morel and Nagaraj (1993). We generate each $i=1,2,...,n$, using equation (7.32).

As discussed in this chapter, the two distributions are strictly different, they are both
overdispersed relative Multinomial distribution and have the same mean and variances.
In simulation and in Monte Carlo studies where the interest is in correlated
multomial responses with first two moments in (7.28) and (7.29), the algorithm in equation
(7.32) is simpler and faster than the algorithm for generating Dirichlet-multinomial responses.

```
/* Generation of data under the Dirichlet-multinomial and
Random-clamped Multinomial distributions
with parameters Pi(1), Pi(2),...,Pi(d), Rho and m
*/
```

```
ods html;
proc imml;
nd = 3;
pi_1 = 0.4;
pi_2 = 0.3;
pi_3 = 0.2;
rho = 0.5;
m = 10;
n = 20000;

pi = pi_1|pi_2|pi_3;
TrueMean = m*Pi;
TrueCov = m*(diag(Pi))*pi'*pi*(1+(m-1)*rho*rho);
print 'True Mean and Covariance under Dirichlet-multinomial and Random-
clumpMultinomial Models';
print True_Mean[format=8.4],True_Cov[format=8.4];

tdm = j(n,d);
trcm = j(n,d);
pi_4 = 1-pi_1-pi_2-pi_3;
pi = pi || pi_4;
call randseed(1914);
---- Generation data under the Dirichlet-multinomial distribution;
c = i/rho;
shape = c*pi;
```
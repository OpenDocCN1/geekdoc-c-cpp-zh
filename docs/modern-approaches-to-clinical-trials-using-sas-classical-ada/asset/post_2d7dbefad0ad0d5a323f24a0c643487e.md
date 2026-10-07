
## Table 9.11 Neyman and Optimal Randomization Assignments

| Randomization Scheme | Allocation probability to Arm | Next Assignment |
|---|---|---|
| Neyman | 0.4850509 | B |
| Optimal | 0.5743003 | B |

There is a tradeoff between minimizing the expected number of treatment failures (nonresponses) and maximizing the power of hypothesis testing. To select a suitable randomization scheme for a clinical trial, simulation studies need to be conducted to compare several different adaptive randomization procedures. For illustration, we consider a two-arm clinical trial with binary responses. The sample size $n$ for each pair of $p_1$ and $p_2$ is determined to yield a I error rate of 0.05 (two-sided) and a power of 0.90 under equal allocation. We investigate the performance of four adaptive-randomization procedures: the equal randomization, the randomized play-the-winner rule (RPW) with $\alpha=1$ and $m=0$, Neyman's allocation procedure, and the optimal adaptive scheme (Opt) that minimizes the total number of nonresponders.

The SAS macro rarsim (available from supplemental website) simulates 5000 replications (nsim=5000) under each scenario. Tables 9.12-9.14 summarize the operating characteristics of the four adaptive randomization methods, which includes the mean of the allocation proportions to treatment 1, i.e., $n1/n$ (Table 9.12), the power of the hypothesis test (Table 9.13), and the expected number of treatment failures (Table 9.14). Standard deviations are in parentheses.

## Table 9.12 Simulation Study of Response Adaptive Randomization Procedures (n1/n)

| $p_1$ | $p_2$ | $n$ | Opt | Neyman | RPW | Equal |
|---|---|---|---|---|---|---|
| 0.2 | 0.2 | 200 | 0.50 (0.05) | 0.50 (0.05) | 0.50 (0.03) | 0.50 (0.04) |
| 0.5 | 0.5 | 200 | 0.50 (0.04) | 0.50 (0.04) | 0.50 (0.03) | 0.50 (0.03) |
| 0.2 | 0.3 | 784 | 0.45 (0.03) | 0.47 (0.02) | 0.47 (0.02) | 0.50 (0.02) |
| 0.2 | 0.4 | 218 | 0.42 (0.05) | 0.45 (0.04) | 0.43 (0.04) | 0.50 (0.03) |
| 0.4 | 0.6 | 260 | 0.45 (0.04) | 0.50 (0.03) | 0.40 (0.05) | 0.50 (0.03) |
| 0.4 | 0.7 | 112 | 0.44 (0.06) | 0.52 (0.05) | 0.33 (0.09) | 0.50 (0.05) |
| 0.6 | 0.8 | 218 | 0.46 (0.04) | 0.54 (0.04) | 0.34 (0.10) | 0.50 (0.03) |

## Table 9.13 Simulation Study of Response Adaptive Randomization Procedures (Power)

| $p_1$ | $p_2$ | $n$ | Opt | Neyman | RPW | Equal |
|---|---|---|---|---|---|---|
| 0.2 | 0.2 | 200 | 0.04 | 0.05 | 0.05 | 0.04 |
| 0.5 | 0.5 | 200 | 0.04 | 0.05 | 0.04 | 0.04 |
| 0.2 | 0.3 | 784 | 0.90 | 0.90 | 0.90 | 0.90 |
| 0.2 | 0.4 | 218 | 0.90 | 0.89 | 0.89 | 0.90 |
| 0.4 | 0.6 | 260 | 0.90 | 0.90 | 0.88 | 0.90 |
| 0.4 | 0.7 | 112 | 0.90 | 0.88 | 0.87 | 0.90 |
| 0.6 | 0.8 | 218 | 0.90 | 0.89 | 0.86 | 0.90 |

## Table 9.14 Simulation Study of Response Adaptive Randomization Procedures (Treatment Failures)

| $p_1$ | $p_2$ | $n$ | Opt | Neyman | RPW | Equal |
|---|---|---|---|---|---|---|
| 0.2 | 0.2 | 200 | 159.9 (5.6) | 159.9 (5.6) | 159.9 (5.7) | 159.9 (5.7) |
| 0.5 | 0.5 | 200 | 100.0 (7.1) | 100.0 (6.9) | 99.9 (7.1) | 99.9 (7.1) |
| 0.2 | 0.3 | 784 | 584.3 (12.5) | 585.6 (11.9) | 585.1 (12.3) | 585.1 (12.3) |
| 0.2 | 0.4 | 218 | 149.0 (6.9) | 150.5 (6.6) | 149.4 (7.1) | 149.4 (7.1) |
| 0.4 | 0.6 | 260 | 127.4 (8.0) | 129.9 (7.7) | 124.7 (8.7) | 124.7 (8.7) |
| 0.4 | 0.7 | 112 | 148.2 (5.1) | 150.9 (4.9) | 144.7 (6.2) | 144.7 (6.2) |
| 0.6 | 0.8 | 218 | 163.8 (6.5) | 167.2 (6.6) | 158.4 (7.9) | 158.4 (7.9) |

Based on the results, it is clear that the randomized play-the-winner rule assigns more patients to the better treatment. However, Neyman's allocation is unethical when $p_1 < p_2$ because it assigns more patients to the worse treatment. In contrast, the optimal adaptive design performs well in terms of power.

## Example 9.9 Bayesian Adaptive Randomization

```sas
%macro BayesianRandomize(n1,n2,y1,y2,alpha=0.5,alpha2=0.5,gamma=1,seed=123);
 proc iml
 call randseed(&seed);
 /* Posterior probability that A is superior to B */
/* Using MCMC approximation to compute the probability */
 postb=j(1000,1)
 call randgen(posta, "BETA", gamma+alpha,n1-y1+beta);
 call randgen(postb, "BETA", gamma+alpha2,n2-y2+beta);
 lambda=sum(postb)/1000;

 if design=1 then Gamma=Gamma
 else Gamma=(n1+n2)/2;

 pi=Gamma/(GammaGamma1-lambdalambda-gamma)
 Assignment=j(1);
 call randgen(Assignment, "BERNOULLI",pi);
 if Assignment=1 then Assignment='A';
 else Assignment='B';
 Print Gamma[colname="Allocation probability to arm A" label=""]
 Assignment[colname="Next assignment" label=""]
 quit;
%end BayesianRandomize;

 BayesianRandomize(n1=20,n2=13,y1=14,y2=5,alpha=0.5,alpha2=0.5,gamma=1,seed=123);
 BayesianRandomize(n1=20,n2=13,y1=14,y2=5,alpha=0.5,alpha2=0.5,gamma=2,n=150,seed=123);
```

## Table 9.15 Output from Example 9.9

| | Allocation Probability to Arm A | Next Assignment |
|---|---|---|
| 1 | 0.9618 | A |
| 0.11 | 0.5878 | B |

Although RAR can help mitigate ethical issues, it may cause an imbalance among the prognostic factors across different groups. For a more balanced design, covariate-adjusted and response-adaptive randomization procedures can be used to address concerns with both response and covariates. Under such a randomization scheme, the allocation probability is skewed to more effective treatments, and the distributions of the covariates are simultaneously adjusted toward balance [17, 18].

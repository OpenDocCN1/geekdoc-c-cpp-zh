distributions for the success probabilities under the two treatment groups, respectively.

+   3. design is the design parameter, design=1 means using a constant tuning parameter. If design=1 is utilized, it requires that you specify the value of γ. On the other hand, design=2 allows γ to vary with the sample size, i.e., γn = n/2N. Users need to input the maximum sample size (n) if design=2.

We illustrate the method by setting a constant γ=1, as well as varying γ in Example Code 9.9 Bayesian Response Adaptive Randomization. Results are summarized in Output from Example Code 9.9.

# Example Code 9.9 Bayesian Response Adaptive Randomization

```
%macro BayesianRandomize(n1,n2,y1,y2,beta=0.5,alpha2=0.5,gamma=1,seed=123)
 proc iml
 call randseed(&seed);
  /* Posterior probability that treatment A is superior to treatment B */
  /* Using MCMC approximation to compute the probability */
 postb=j(1000,1)
 call randgen(posta, "BETA", gamma+1&alpha,nl-1&yl1+&beta);
 call randgen(postb, "BETA", gamma+2&alpha2,n2-y2+&beta);
 lambda=sum(postb)/1000;

 if design=1 then Gamma=Gamma
 else Gamma=(n1+n2)/2;

 pi=Gamma##Gamma/(lambda##Gamma) (1-lambda)##Gamma)
 Assignment=j(1);
 call randgen(Assignment, "BERNOULLI",pi);
 if Assignment=1 then Assignment='A';
 else Assignment='B';
 Print Gamma[colname="Allocation probability to arm A" label=""]
 Assignment[colname="Next assignment" label=""]
 quit;
%end BayesianRandomize(n1=20,y1=14,n2=13,y2=5,alpha=0.5,alpha2=0.5,beta2=0.5,design=1,gamma=1,seed=123)
 BayesianRandomize(n1=20,y1=14,n2=13,y2=5,alpha=0.5,alpha2=0.5,beta2=0.5,design=2,n=150,seed=123)
```

Table 9.15 Output from Example 9.9

| | Allocation Probability to Arm A | Next Assignment |
|---|---|-|
| 1 | 0.9618 | A |
| 0.11 | 0.5878 | B |

459
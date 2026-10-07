
probability p = 0.75 (Example Code 9.5 Covariate-Adaptive Allocation by Minimization).

## Example Code 9.5 Covariate-Adaptive Allocation by Minimization

```sas
data FactorWeight;
input w;
datalines;
1
1
;
run;

%macro MinimizationRandomize(TreatedPatients,NewPatient,FactorWeight,p,seed);
proc ilm;
use &TreatedPatients;
read all into X;
use &TreatedPatients;
read all var (group);
use &NewPatient;
read all into Y;
use &FactorWeight;
read all;
call randseed(&seed);
X=X//Y;

imA=0;
groupA=group//'A';
do i=1 to ncol(X);
  do j=1 to max(X[i,j]);
    imA=imA+w[i]*abs(sum(groupA[loc(X,[i,j])='A'])-sum(groupA[loc(X,[i,j])='B']));
  end;
end;
nimB=0;
groupB=group//'B';
do i=1 to ncol(X);
  do j=1 to max(X[i,j]);
    imB=imB+w[i]*abs(sum(groupB[loc(X,[i,j])='A'])-sum(groupB[loc(X,[i,j])='B']));
  end;
end;
print imA imB;

nu=1;
call randgen(u, "Uniform");

if (imA<imB & u<=p) then
call symput('newgroup', 'A');
if (imA>=imB & u<=p) then
call symput('newgroup', 'B');
if (imA<imB & u>p) then
call symput('newgroup', 'B');
if (imA>imB & u>p) then
call symput('newgroup', 'A');

NextGroup=sumget('newgroup');
print NextGroup;
quit;
```

```sas
data &NewPatient;
  length group $;
  group=symget("newgroup");
  set &NewPatient;
run;
```

```sas
proc data=\&TreatedPatients;
run;

data &TreatedPatients;
  set &TreatedPatients. &Newpatient;
run;
```

```sas
proc data=\&TreatedPatients;
run;
%mend MinimizationRandomize;
```

- * 1st subject: male, tumor I
  data NewPatient;
  input gender tumororage;
  datalines;
  1 1

```sas
%MinimizationRandomize(TreatedPatients,NewPatient,FactorWeight,p=0.75,seed=6)
```

- * 2nd subject: male, tumor II
  data NewPatient;
  input gender tumororage;
  datalines;
  1 2

```sas
%MinimizationRandomize(TreatedPatients,NewPatient,FactorWeight,p=0.75,seed=6)
```

- * 3rd subject: female, tumor II
  data NewPatient;
  input gender tumororage;
  datalines;
  2 2

```sas
%MinimizationRandomize(TreatedPatients,NewPatient,FactorWeight,p=0.75,seed=6)
```

The macro produces a set of outputs. First, it provides the total imbalance, when the new patient is assigned to group A and B, Second, the macro would suggest a group for the new subject based on the minimization method. Last, the TreatedPatients data set is updated by including the data of the new patient. The full outputs for the example above are omitted here, when we summarize the results of randomization in Output from Example Code 9.5.

### Table 9.8 Output from Example Code 9.5

| Sub | Treatment | Sex | Imbalance (assigned to A) | Imbalance (assigned to B) |
|---|---|---|---|---|
| 1 | B | Male | 12 | 8 |
| 2 | A | Male | 8 | 8 |
| 3 | A | Female | 6 | 10 |

Therefore, to minimize the total imbalance, the first subject should be assigned to treatment B. For the second subject, the total imbalance is the same regardless of whether this participant is assigned to treatment A or B. As a result, we can choose a treatment purely at random. Clearly, the third subject would receive treatment A so as to minimize the total imbalance.

## 9.4.3 Model-Based Optimal Covariate-Adaptive Randomization

To implement the minimization method, continuous covariates need to be categorized. However, it is often arbitrary to determine the number of categories and the corresponding cutoff values. As an alternative, one can develop an optimal randomization procedure such that the variance of the estimated treatment effect in the presence of covariates is minimized. Specifically, let $Y_j$ be the outcome of the $j$th patient, $X_j$ be the $p$-dimensional covariates (including the intercept), $Z_j$ be the treatment indicator that takes a value of 1 if the $j$th patient is assigned to the treatment group, and -1 if to the control group. For continuous outcome $Y_j$, we assume a linear model,

$$$$Y_j = X_j^T \beta + Z_j \epsilon_j.$$

where $\epsilon_j$ is the random error that follows a normal distribution with mean 0 and variance $\sigma^2$, $\beta$ and $\zeta$ are the parameters to be estimated with $\zeta$ denoting the treatment effect. The variance of the estimated treatment effect is

$$$$Var(\hat{\zeta}) = \frac{\sigma^2}{n-Z^TX(X^TX)^{-1}X^TZ}.$$

where $X$ denotes the $n \times p$ matrix of covariates and $Z$ is the $n \times 1$ vector of $Z_j, j=1..n$. Therefore, minimizing $Var(\hat{\zeta})$ can be achieved by minimizing the loss function

$$$$\mathcal{L}_n = Z^TX(X^TX)^{-1}X^TZ.$$

which can be interpreted as the number of units lost due to inefficiency of treatment allocation.

Suppose that $n$ patients have already been assigned to the two treatment groups, and the covariates $X_{n+1}$ of the $(n+1)$th patient have been collected. To construct a sequential procedure, the treatment assignment of the $(n+1)$th patient is chosen to minimize the loss $\mathcal{L}_{n+1}$ with high probability. For example, the probability that the $(n+1)$th patient is assigned to the treatment group can be specified as

$$Pr(Z_{n+1}=1|R_{n+1}) = \frac{X_{n+1}^T(X^TX)^{-1}X^TZ}{1 + \gamma X_{n+1}^T(X^TX)^{-1}X^TZ}$$

where $\gamma \ge 0$ is a prescribed tuning parameter to control the degree of randomness. Obviously, if $\gamma = 0$, the procedure reduces to equal randomization; Typically, $\gamma = 5$ is recommended to achieve balance between the treatment groups and the loss. Suppose that $n$ patients have already been assigned to the two treatment groups, and the covariates $X_{n+1}$ of the $(n+1)$th patient have been collected. To illustrate the model-based CAR, we apply it to assign patients based on their prognostic factors. Once $n$ patients have been enrolled, the model-based CAR updates the TreatedPatients data set by including the data of the new patient. The output from Example Code 9.6 shows:

### Example Code 9.6 Model-Based CAR

```sas
proc data=\&TreatedPatients;
run;
```

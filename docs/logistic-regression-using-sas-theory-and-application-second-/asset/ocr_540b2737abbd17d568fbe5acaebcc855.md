Using the REG procedure in SAS, I estimated a linear regression model that uses DEATH as the dependent variable and the other three as independent variables. The SAS code is

```
```sas
PROC REG DATA=penalty;
   MODEL death=blackd whitic serious;
RUN;
```
```

Results are shown in Output 2.1. Neither of the two racial variables have coefficients that are significantly different from 0. Not surprisingly, the coefficient for SERIOUS is highly significant—more serious crimes are more likely to get the death penalty.

Should we trust these results, or should we ignore them because the statistical technique is incorrect? To answer that question we need to see *why* linear regression is regarded as inappropriate when the dependent variable is a dichotomy. That’s the task of the next section.

# Output 2.1  Linear Regression of Death Penalty on Selected Independent Variables

|  |  |
|---|---:|
| **Number of Observations Read** | 147 |
| **Number of Observations Used** | 147 |

### Analysis of Variance

| Source | DF | Sum of Squares | Mean Square | F Value | Pr > F |
|---|---:|---:|---:|---:|---:|
| Model | 3 | 2.61611 | 0.87204 | 4.11 | 0.0079 |
| Error | 143 | 30.37709 | 0.21243 |  |  |
| Corrected Total | 146 | 32.99320 |  |  |  |

|  |  |  |  |
|---|---:|---|---:|
| **Root MSE** | 0.46090 | **R-Square** | 0.0793 |
| **Dependent Mean** | 0.34014 | **Adj R-Sq** | 0.0600 |
| **Coeff Var** | 135.50409 |  |  |
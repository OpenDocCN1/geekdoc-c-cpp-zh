# 7.5 Modeling results

Seven crews rowed the four tests each. The number of data was 28. It was not large. So, to prevent the model from over-fitting to the data, two factors out of three were used to infer the average boat speed.

First, x = (Total Work, Power Consistency) were used as the inputs. The input and output data were normalized in the range [0,1]. Table 7.1 shows the result obtained by the linear regression. Table 7.2 shows the result of the fuzzy modeling. In this table, the membership functions and the singletons in the consequent were labeled with S for Small, M for Medium, L for Large. These linguistic rules are easy to understand for coaches and athletes. The rules were reasonable. The more the total work was given, the faster the boat speed became. In the case where the total work was large and the consistency was high, the boat speed was very high. Nonlinear relationships were revealed by this model. The consistency did not affect the boat speed if the total work was not large. It had an effect only if the total work was large.

| MSE | 0.035 |
| Knowledge | y = 0.84x₁ + 0.36x₂ |

Table 7.1 Result of Linear Regression

| MSE | 0.016 |
| Knowledge | If x₁ is S, then y is MS. |
|  | If x₁ is MS, then y is ML. |
|  | If x₁ is ML, then y is ML. |
|  | If x₁ is L and x₂ is Not L, then y is L. |
|  | If x₁ is L and x₂ is L, then y is Very L. |

Table 7.2 Result of Fuzzy Modeling

Figure 7.6 shows the division of the input space. Figures 7.7 and 7.8 show the membership functions for the total work and the power consistency, respectively.

Next, x = (Total Work, Power Uniformity) were used as the inputs. Table 7.3 shows the result obtained by the linear regression. Table 7.4 shows the result of the fuzzy modeling. These rules were also reasonable. The more the total work was given, the faster the boat speed became. But, the fourth rule
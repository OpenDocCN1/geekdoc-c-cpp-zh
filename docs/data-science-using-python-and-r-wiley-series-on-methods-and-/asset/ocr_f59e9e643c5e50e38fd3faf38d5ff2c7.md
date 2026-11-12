| | coef | std err | z | P>|z| | [0.025 | 0.975] |
|---|---|---|---|---|---|---|
| const | 0.3714 | 0.016 | 23.877 | 0.000 | 0.341 | 0.402 |
| Churn = True | 0.4305 | 0.034 | 12.582 | 0.000 | 0.363 | 0.498 |

Figure 13.5 Python Poisson regression results for predicting number of customer service calls.

The structure of our Poisson regression model will be

$CustServ Calls = \exp(b_0 + b_1(Churn))$

The result of the regression analysis is given in Figure 13.5. Using the coefficients given above, we can build the Poisson regression model

$CustServ Calls = \exp(0.3714 + 0.4305(Churn = True))$

Now, how do we interpret the Poisson regression coefficients? When used as the exponent of e, the regression coefficient describes the estimated multiplicative change in the response variable when the coefficient's predictor variable increases by one. In our case, the regression coefficient is 0.4305, which gives us $e^{0.4305} = 1.538$. The coefficient's predictor, Churn, is zero if the customer does not churn and one if they do. Therefore, the movement from a non-churning to churning customer increases the predicted number of customer service calls that customer makes by 1.538 times, or 53.8 %.

# 13.6.1 How to Perform Poisson Regression Using Python

Naturally, in order to validate our modeling results, you would first split the data into training and test data sets. As cross-validation has been shown in other chapters as well as for logistic regression, we restrict this section to illustrating how to build the Poisson regression model.

Load the required packages.

```
import pandas as pd
import numpy as np
import statsmodels.api as sm
import statsmodels.tools.tools as stattools
```

Read in the churn data set into Python as churn.

```
churn = pd.read_csv("C:/.../churn")
```

Our predictor variable is Churn, which is categorical. Similar to previous modeling tasks, we need to change the categorical values of Churn into dummy
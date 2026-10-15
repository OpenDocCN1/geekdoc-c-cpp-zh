```
In [1]: import pandas as pd
import numpy as np

starbucks = pd.read_csv("profile.csv", index_col=0)
starbucks.dropna(inplace=True)
starbucks['became_member_on'] = pd.to_datetime(starbucks['became_member_on'], format='%Y%m%d')
starbucks.head()
```

Out[1]:
| gender | age | id | became_member_on | income |
|---|---|---|---|---|
| 1 | F | 55 | 0610b486422d4921ae7d2bf64640c50b | 2017-07-15 | 112000.0 |
| 3 | F | 75 | 78afa995795e4d85b5d9ceeca43f5fef | 2017-05-09 | 100000.0 |
| 5 | M | 68 | e2127556f4f64592b11af22de27a7932 | 2018-04-26 | 70000.0 |
| 8 | M | 65 | 389bc3fa690240e798340f5a15918d5c | 2018-02-09 | 53000.0 |
| 12 | M | 58 | 2eeac8d8feae4a8cad5a6af0499a211d | 2017-11-11 | 51000.0 |

Columns description:

+   - gender : Gender of the customer (note some entries contain 'O' for other rather than M or F)
+   - age : Age of the customer
+   - id : Customer id
+   - became_member_on : Date when customer created an app account
+   - income : Customer's income

The main difference between these models and our first three clustering models is that we do not specify how many clusters we want.

1. What do we want to obtain?

K groups of customers and their caracterization.

2. What type of data is?

Categorical, qualitative. Client Type 1, 2, 3, ... k

Type 1 Clients like to... are mostly ...

3. Which data are we going to use to create the clusters?

+   - gender : (qualitative, nominal)
+   - age : (Numerical, quantitative continuous)
+   - became_member_on : (Numerical, quantitative continuous)
+   - income : (Numerical, quantitative continuous)
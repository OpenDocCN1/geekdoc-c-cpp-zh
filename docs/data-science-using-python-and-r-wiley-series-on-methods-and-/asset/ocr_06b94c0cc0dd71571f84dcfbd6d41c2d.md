| | RC1 | RC2 | RC3 | RC4 |
|---|---|---|---|---|
| Days.since.Purchase | | | 0.932 | |
| Purchase.Visits | 0.891 | | | |
| Days.on.File | | 0.965 | | |
| Days.between.Purchases | | | | 0.901 |
| Diff.items.Purchased | 0.944 | | | |

Figure 12.12 Component weights from R for the test data set.

```
> round(cor(pca02_rot$scores),2)
```

| | RC1 | RC2 | RC3 | RC4 |
|---|---|---|---|---|
| RC1 | 1 | 0 | 0 | 0 |
| RC2 | 1 | 0 | 0 | 0 |
| RC3 | 0 | 0 | 1 | 0 |
| RC4 | 0 | 0 | 0 | 1 |

Figure 12.13 R output showing the principal components are uncorrelated.

```
> vif(model.pca)
```

```
PC1 PC2 PC3 PC4
1 1 1 1
```

Figure 12.14 R output showing that regression using the principal components eliminates multicollinearity.

results in Figure 12.8. The four rotated components for the test set, shown in Figure 12.12, are similar to those for the training set from Figure 12.10b. So, did PCA alleviate our multicollinearity problem? We can check by examining

+   1. The correlations among the four components.
+   2. The predictor VIF for the regression of the response on the components.

The correlation matrix for the principal components is shown in Figure 12.13. All correlations are zero, meaning that the components are uncorrelated. Finally, we obtain the VIFs for the regression of Sales per Visit on the four extracted principal components substituted for the original predictors. These VIFs results shown in Figure 12.14 indicate that all VIFs equal 1, the minimum.

# 12.9 HOW TO PERFORM PRINCIPAL COMPONENTS ANALYSIS USING PYTHON

Load the required packages.

```
import pandas as pd
import numpy as np
from sklearn.preprocessing import StandardScaler
from sklearn.decomposition import PCA
```
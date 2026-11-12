most of the data values are near 1000, with a minority of values near zero. It turns out that the database administrator used the code 999 to represent customers who had not been contacted previously. Thus, we need to change the field value 999 to missing, which is done as follows in Python and R.

# ## 3.5.1 How to Change Misleading Field Values Using Python

If you did not open the `pandas` package or read in the data set, as described in the previous Python section, do so now. We also need to import the `numpy` package for this section.

```
import numpy as np
```

We need to identify all records with `days_since_previous` value of 999 and replace them with the Python code for missing numbers, `NaN`. Once the replacement is made, we will save the variable under the `days_since_previous` variable name, effectively overriding the previous variable’s values.

```
bank_train['days_since_previous'] = bank_train['days_since_previous'].replace({999: np.NaN})
```

The code `bank_train['days_since_previous']` accesses the variable `days_since_previous`. The command `replace({999: np.NaN})` finds each instance of 999 in the `days_since_previous` variable and replaces it with the value `NaN`. To save the newly edited variable under its original name, we set the right-hand side equal to the original `days_since_previous` variable on the left by reusing the variable name `bank_train['days_since_previous']`.

To create a histogram of the variable, use the `hist()` command.

```
bank_train['days_since_previous'].plot(kind = 'hist', title = 'Histogram of Days Since Previous')
```

Using `.plot()` after the variable name will make a plot of the variable. We use `kind = 'hist'` to specify that a histogram should be made. The `title` input, contained in single quotes, creates the title of the histogram. The output is shown in Figure 3.2. In Chapter 4, we will look at more complex histograms.

# ## 3.5.2 How to Change Misleading Field Values Using R

If you did not read in the data set, as described in the previous R section, do so now.

We need to identify each instance of 999 in the `days_since_previous` variable, and replace it with the R code value for a missing value, `NA`.
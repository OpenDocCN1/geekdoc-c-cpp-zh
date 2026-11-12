numeric fields as a matter of course. Next, we show how to standardize numeric fields in Python and R.

# 3.7.1 How to Standardize Numeric Fields Using Python

Import the required package.

```
from scipy import stats
```

We will standardize the age variable and save it as a new variable, age_z.

```
bank_train['age_z'] = stats.zscore(bank_train['age'])
```

The zscore function calculates the z-value of the given variable, in this case age, written in the code as bank_train['age']. As the zscore() command is part of the stats package, we write the command as stats.zscore(). We save it as a new variable in the data set, age_z.

# 3.7.2 How to Standardize Numeric Fields Using R

We do not have to install or load a package for this code. The command we will use, scale(), is included in the initial download of R.

```
bank_train$age_z <- scale(x = bank_train$age)
```

The scale() function can center a variable by subtracting its mean, scale it by dividing by the standard deviation, or both. By default, it does both, as needed to calculate the z-score. Thus, using the default settings of the scale() function on the bank_train$age variable will return the z-scores of the variable. We can save the z-values as a new variable in the data set using bank_train$age_z.

# 3.8 IDENTIFYING OUTLIERS

Once the numeric fields are standardized, one may use the z-values to identify outliers, which are records with extreme values along a particular dimension or dimensions. For example, consider the field number_of_contacts, which represents the number of customer contacts made over the course of the marketing campaign. The mean number of contacts per customer is 2.6, with a standard deviation of 2.7 (allowing for rounding). So, we obtain the standardized field as follows:

number_of_contacts_z = \frac{number\_of\_contacts - 2.6}{2.7}
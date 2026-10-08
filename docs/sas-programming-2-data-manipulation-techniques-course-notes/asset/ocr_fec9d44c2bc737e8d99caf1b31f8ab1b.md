# Check the SAS Log

Three data sets were created. The log shows that US was the most frequently occurring value.

# Partial SAS Log

```
NOTE: There were 424 observations read from the data set
ORION.EMPLOYEE_ADDRESSES.
NOTE: The data set WORK.USA has 311 observations and 9 variables.
NOTE: The data set WORK.AUSTRALIA has 105 observations and 9 variables.
NOTE: The data set WORK.OTHER has 6 observations and 9 variables.
```

# Efficient Conditional Processing

It is more efficient to check values in order of decreasing frequency

```
data usa australia other;
set orion.employee addresses;
if Country='US' then output usa;
else if Country='AU' then output australia;
else output other;
run;
```

```
NOTE: There were 424 observations read from the data set
ORION.EMPLOYEE_ADDRESSES.
NOTE: The data set WORK.USA has 311 observations and 9 variables.
NOTE: The data set WORK.AUSTRALIA has 105 observations and 9 variables.
NOTE: The data set WORK.OTHER has 6 observations and 9 variables.
```
# Using the DROP= Data Set Option

```
data usa(drop=Street ID Country)
australia(drop=Street_ID State Country)
other;
set orion.employee_addresses;
if Country='US' then output usa;
else if Country='AU' then
  output australia;
else output other;
run;
```

NOTE: There were 424 observations read from the data set
ORION.EMPLOYEE_ADDRESSES.
NOTE: The data set WORK.USA has 311 observations
and 2 variables.
NOTE: The data set WORK.AUSTRALIA has 105 observations
and 6 variables.
NOTE: The data set WORK.OTHER has 8 observations
and 9 variables.

![](bbox=[0.565, 0.395, 0.625, 0.405])

# KEEP= Option in an Output Data Set

```
SAS-data-set(KEEP=variable-1 <variable-2 ...variable-n>)
```

new1

| Y | Z |
|---|---|

old data new1(keep=y z)
new2(drop=x z)
new3;
set old;
...

PDV
| X | Y | Z |
|---|---|---|

| X | Y | Z |
|---|---|---|

new2

| X | Y | Z |
|---|---|---|

new3

| X | Y | Z |
|---|---|---|

![](bbox=[0.435, 0.585, 0.715, 0.665])
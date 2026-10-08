# Controlling Variable Output (Review)

In the DATA step, the DROP and KEEP statements can be used to control which variables are written to output data sets. The statements can be used when reading from a SAS data set or from a raw data file.

```
data out1 out2;
set in;
drop x;

out1
Y Z
...
PDV
X Y Z

out2
Y Z
```

# DROP Statement

The DROP statement drops variables from every output set.

```
data usa australia other;
drop Street ID;
set orion.employee_addresses;
if Country='US' then output usa;
else if Country='AU' then output australia;
else output other;
run;
```

Partial SAS Log

NOTE: There were 424 observations read from the data set
ORION.EMPLOYEE_ADDRESSES.
NOTE: The data set WORK.USA has 311 observations and 8 variables.
NOTE: The data set WORK.AUSTRALIA has 105 observations and 8 variables.
NOTE: The data set WORK.OTHER has 8 observations and 8 variables.
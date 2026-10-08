
# Execution: Performing Repetitive Calculations

```
data invest;
do Year=2008 to 2010;
  Capital+5000;
  Capital+(Capital*.045);
end;
run;
```

![](img/d3bde6e6ab06b1fc622215d982111742_286_0.png)

| Year | Capital | N |
|---|---|--|
| 2008 | 5000 | |

# Execution: Performing Repetitive Calculations

```
data invest;
do Year=2008 to 2010;
  Capital+5000;
  Capital+(Capital*.045);
end;
run;
```

![](img/d3bde6e6ab06b1fc622215d982111742_286_1.png)

| Year | Capital | N |
|---|---|--|
| 2008 | 5225 | |

# Execution: Performing Repetitive Calculations

```
data invest;
do Year=2008 to 2010;
  Capital=5000;
  Capital+(Capital*.045);
end;
run;
```

![](img/d3bde6e6ab06b1fc622215d982111742_287_0.png)

# Execution: Performing Repetitive Calculations

```
data invest;
do Year=2008 to 2010;
  Capital=5000;
  Capital+(Capital*.045);
end;
run;
```

![](img/d3bde6e6ab06b1fc622215d982111742_287_1.png)

| Year | Capital | N |
| 2009 | 5225 | 1 |

# 7.1 DO Loop Processing 7-11

# Execution: Performing Repetitive Calculations

```
data invest;
do Year=2008 to 2010;
  Capital+5000;
  Capital+(Capital* .045);
end;
run;
```

![](img/d3bde6e6ab06b1fc622215d982111742_288_0.png)

| Year | Capital | N |
|---|---|--|
| 2009 | 10225 | 1 |

20

# Execution: Performing Repetitive Calculations

```
data invest;
do Year=2008 to 2010;
  Capital+5000;
  Capital+(Capital* .045);
end;
run;
```

![](img/d3bde6e6ab06b1fc622215d982111742_288_1.png)

| Year | Capital | N |
|---|---|--|
| 2009 | 10685.13 | 1 |

21

Copyright © 2014, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED.

# Execution: Performing Repetitive Calculations

```
data invest;
do Year=2008 to 2010;
  Capital+=5000;
  Capital+(Capital*.045);
end;
```

![](img/d3bde6e6ab06b1fc622215d982111742_289_0.png)

# Execution: Performing Repetitive Calculations

```
data invest;
do Year=2008 to 2010;
  Capital+=5000;
  Capital+(Capital*.045);
end;
```

![](img/d3bde6e6ab06b1fc622215d982111742_289_1.png)

| Year | Capital | N |
|---|---|---|
| 2010 | 10685.13 | 1 |

# Execution: Performing Repetitive Calculations

```
data invest;
 do Year=2008 to 2010;
  Capital+5000;
  Capital+(Capital*.045);
end;
run;
```

![](img/d3bde6e6ab06b1fc622215d982111742_290_0.png)

| Year | Capital | N |
|---|---|--|
| 2010 | 15685.13 | 1 |

# Execution: Performing Repetitive Calculations

```
data invest;
 do Year=2008 to 2010;
  Capital+5000;
  Capital+(Capital*.045);
end;
run;
```

![](img/d3bde6e6ab06b1fc622215d982111742_290_1.png)

| Year | Capital | N |
|---|---|--|
| 2010 | 16390.96 | 1 |

# Execution: Performing Repetitive Calculations

```
data invest;
do Year=2008 to 2010;
  Capital=5000;
  Capital=Capital*.045;
end;
run;
```

![](img/d3bde6e6ab06b1fc622215d982111742_291_0.png)

# Execution: Performing Repetitive Calculations

```
data invest;
do Year=2008 to 2010;
  Capital=5000;
  Capital=Capital*.045;
end;
run;
```

> Is Year out of range?

![](img/d3bde6e6ab06b1fc622215d982111742_291_1.png)

# Execution: Performing Repetitive Calculations

```
data invest;
  do Year=2008 to 2010;
    Capital+5000;
    Capital+(Capital*.045);
  end;
run;

Output current observation

| Year | Capital | N |
|---|---|---|
| 2011 | 16390.96 | 1 |

# Output: Performing Repetitive Calculations

```
proc print data=invest;
run;
```

PROC PRINT Output

| Year | Capital |
|---|---|
| 2011 | 16390.96 |

# 7.02 Short Answer

How can you generate a separate observation for each year?

```
data invest;
do Year=2008 to 2010;
  Capital=5000;
  Capital+(Capital*.045);
output;
run;
proc print data=invest;
```

# Exercises

If you restarted your SAS session since the last exercise, open and submit the .sas program found in the folder.

# 1. Performing Computations with DO Loops

The Orion Star Department must project total employee costs (wages, retirement benefits, and medical benefits) through future years, based on assumed annual increases shown in the table below.

| Variable | Current Value | Annual Increase |
|---|---|---|
| Wages | $12,874,000 | 6.0% |
| Retire | $1,765,000 | 1.4% |
| Medical | $649 | 9.5% |

# 7.2 Conditional DO Loop

a. Insert a DO loop containing statements to calculate the estimated values of Wages, Retire, and Medical.
- Use Start and Stop to control the values of the Year variable. For example, to calculate Wages using this formula:
- Create another variable, Total_Cost, as the sum of that year's Wages, Retire, and Medical.
- Output one observation for year. Your report should contain 10 observations.
b. Print and verify your results.

Partial PROC Output (10 Observations)

| Obs | Year | Wages | Medical | Total_Cost |
|---|---|---|---|---|
| 1 | 2013 | 13,646,440.00 | 1,789,710.00 | 710,655.00 | 16,146,805.00 |
| 2 | 2014 | 14,465,226.40 | 1,814,765.94 | 778,167.23 | 17,058,159.57 |
| 3 | 2015 | 15,333,139.98 | 1,840,172.66 | 852,093.11 | 18,025,405.76 |
| 4 | 2016 | 16,253,128.38 | 1,865,935.08 | 933,041.96 | 19,052,105.42 |
| 5 | 2017 | 17,228,316.09 | 1,892,058.17 | 1,021,680.94 | 20,142,055.20 |

> The results above were generated on February 14, 2012. Your values for Year might differ.

# Business Scenario

Recall the example that forecasts the growth of several departments at Orion Star. Modify the forecasting application to use a DO loop to eliminate redundant code.

Listing of orion.growth

| Department | Total Employees | Increase |
|---|---|---|
| Administration Engineering | 34,999 | 0.25 0.30 |
| IS | 255 | 0.10 |
| Marketing | 200 | 0.20 |
| Sales Management | 20,111 | 0.30 0.10 |

# A Forecasting Application (Review)

```
data forecast;
set orion.growth;
Year=1;
Total_Employees=Total_Employees*(1+Increase);
output;
Year=2;
Total_Employees=Total_Employees*(1+Increase);
output;
```

```
run;
proc print data=forecast noobs;
run;
```

What if you want to forecast growth over the next six years?

# 7.2 Conditional DO Loop Processing

# Use a DO Loop to Reduce Redundant Code

```
data forecast;
  set orion.growth;
  do Year=1 to 6;
    Total_Employees=
    Total_Employees*(1+Increase);
    output;
  end;
run;

proc print data=forecast noobs;
run;
```

# Output

Partial PROC PRINT Output (36 Total Observations)

| Department | Total Employees | Increase | Year |
|---|---|---|---|
| Administration | 42,500 | 0.25 | 1 |
| Administration | 53,125 | 0.25 | 2 |
| Administration | 66,406 | 0.25 | 3 |
| Administration | 83,008 | 0.25 | 4 |
| Administration | 103,760 | 0.25 | 5 |
| Administration | 129,700 | 0.25 | 6 |
| Engineering | 34,999 | 0.30 | 1 |
| Engineering | 45,499 | 0.30 | 2 |
| Engineering | 59,148 | 0.30 | 3 |
| Engineering | 76,893 | 0.30 | 4 |
| Engineering | 99,961 | 0.30 | 5 |
| Engineering | 129,949 | 0.30 | 6 |
| IS | 255 | 0.10 | 1 |
| IS | 281 | 0.10 | 2 |
| IS | 309 | 0.10 | 3 |
| IS | 339 | 0.10 | 4 |
| IS | 373 | 0.10 | 5 |
| IS | 410 | 0.10 | 6 |
| Marketing | 200 | 0.20 | 1 |
| Marketing | 240 | 0.20 | 2 |
| Marketing | 288 | 0.20 | 3 |
| Marketing | 346 | 0.20 | 4 |
| Marketing | 415 | 0.20 | 5 |
| Marketing | 498 | 0.20 | 6 |
| Sales Management | 20,111 | 0.30 | 1 |
| Sales Management | 26,144 | 0.30 | 2 |
| Sales Management | 33,987 | 0.30 | 3 |
| Sales Management | 44,183 | 0.30 | 4 |
| Sales Management | 57,438 | 0.30 | 5 |
| Sales Management | 74,669 | 0.30 | 6 |

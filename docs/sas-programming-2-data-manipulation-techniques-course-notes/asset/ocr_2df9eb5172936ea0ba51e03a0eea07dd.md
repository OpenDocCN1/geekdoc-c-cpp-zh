# Execution: Explicit Output

| Department | Total_Employees | Increase |
| --- | --- | --- |
| Administration | 34 | 0.25 |
| Engineering | 9 | 0.30 |

```
IS data forecast;
set orion.growth;
Year=1;
Total_Employees=Total_Employees*(1+Increase);
output;
Year=2;
Total_Employees=Total_Employees*(1+Increase);
output;
run;
```

| Department | Total_Employees | Increase | Year |
| --- | --- | --- | --- |
| $ 20 | N 8 | N 8 | N 8 |
| Administration | 34 | 0.25 | 1 |

# Execution: Explicit Output

| Department | Total_Employees | Increase |
| --- | --- | --- |
| Administration | 34 | 0.25 |
| Engineering | 9 | 0.30 |

```
IS data forecast;
set orion.growth;
Year=1;
Total_Employees=Total_Employees*(1+Increase);
output;
Year=2;
Total_Employees=Total_Employees*(1+Increase);
output;
run;
34*(1+0.25);
```

| Department | Total_Employees | Increase | Year |
| --- | --- | --- | --- |
| $ 20 | N 8 | N 8 | N 8 |
| Administration | 42.5 | 0.25 | 1 |
# Execution: Explicit Output

orion.growth

```
data forecast;
set orion.growth;
Year-1;
Total_Employees=Total_Employees*(1+Increase);
output;
Year-2;
Total_Employees=Total_Employees*(1+Increase);
output;
```

42.5* (1 + 0.25)

| Department | Total_Employees | Increase | Year |
|---|---|---|---||
| $ 20 | N 8 | N 8 | N 8 |
| Administration | 53.125 | 0.25 | 2 |

# Execution: Explicit Output

orion.growth

| Department | Total_Employees | Increase | Year |
|---|---|---|---|n| Administration | | 34 | 0.25 |
| Engineering | | 9 | 0.30 |
| IS | | | 0 |

```
data forecast;
set orion.growth;
Year-1;
Total_Employees=Total_Employees*(1+Increase);
output;
Year-2;
Total_Employees=Total_Employees*(1+Increase);
output;
```

Output current observation

| Department | Total_Employees | Increase | Year |
|---|---|---|---||
| $ 20 | N 8 | N 8 | N 8 |
| Administration | 53.125 | 0.25 | 2 |
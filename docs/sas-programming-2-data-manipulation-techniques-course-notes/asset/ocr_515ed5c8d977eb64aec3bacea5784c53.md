# Execution: Rotating a SAS Data Set

```
data rotate (keep=Employee Id Period Amount);
set orion.employee donations
(drop=recipients paid by);
array contrib(4) qtr1-qtr4;
doi i=1 to 4
  if contrib(i)ne . then do
    Period=cats("Qtr",i);
    Amount=contrib(i);
    output;
  end
run;
```

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 | Period | Amount |
|---|---|---|---|---|---|-|
| 10267 | 15 | 15 | 15 | 15 | Qtr1 | 15 |

| Employee_ID | Period | Amount |
|---|---|-|
| 10265 | Qtr4 | 25 |

# Execution: Rotating a SAS Data Set

```
data rotate (keep=Employee Id Period Amount);
set orion.employee donations
(drop=recipients paid by);
array contrib(4) qtr1-qtr4;
doi i=1 to 4
  if contrib(i)ne . then do
    Period=cats("Qtr",i);
    Amount=contrib(i);
    output;
  end
run;
```

![](bbox=[0.185, 0.605, 0.455, 0.63])

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 | Period | Amount |
|---|---|---|---|---|---|-|
| 10267 | | | | | Qtr1 | 15 |

| Employee_ID | Period | Amount |
|---|---|-|
| 10265 | Qtr4 | 25 |
| 10267 | Qtr1 | 15 |
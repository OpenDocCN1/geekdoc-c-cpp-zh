# Compilation: Rotating a SAS Data Set

```
data rotate (keep=Employee Id Period Amount);
set orion.employee_donations
  (drop=recipients paid_by);
array contrib(4) qtr1-qtr4;
doi i=1 to 4;
  if contrib(i) ne . then do;
    Period=cats("Qtr",i);
    Amount=contrib(i);
    output;
  end;
run;
```

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 | i | Period | Amount |
|---|---|---|---|---|---|---|---|

| Employee_ID | Period | Amount |
|---|---|---|

# Execution: Rotating a SAS Data Set

```
data rotate (keep=Employee_Id Period Amount);
set orion.employee_donations
n  (drop=recipients paid_by);
array contrib(4) qtr1-qtr4;
doi i=1 to 4;
  if contrib(i) ne . then do;
    Period=cats("Qtr",i);
    Amount=contrib(i);
    output;
  end;
run;
```

![](bbox=[0.485, 0.485, 0.625, 0.535])

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 | i | Period | Amount |
|---|---|---|---|---|---|---|---|

| Employee_ID | Period | Amount |
|---|---|---|
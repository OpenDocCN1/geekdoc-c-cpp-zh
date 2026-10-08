# Execution: Rotating a SAS Data Set

```
data rotate (keep=Employee Id Period Amount);
  set orion.employee donations
  (drop=recipients paid_by);
  array contrib[4] qtr1-q4;
  do i=1 to 4;
    if contrib{i} ne then do
      Period=cats("Qtr",i);
      Amount=contrib{i};
      output;
    end;
  continue Eof;
```

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 | i | Period | Amount |
|---|---|---|---|---|---|---||}{
| 120267 | 15 | 15 | 15 | 15 | | | 15 |

| Employee_ID | Period | Amount |
|---|---|---|n| 120267 | Qtr4 | 25 |
| 120267 | Qtr1 | 15 |

# Output: Rotated Data Set

```
proc print data=rotate;
run;
```

Partial Rotated PROC PRINT Output (417 Total Observations)

| Obs | Employee_ID | Period | Amount |
|---|---|---||}{
| 1 | 120267 | Qtr4 | 25 |
| 2 | 120267 | Qtr1 | 15 |
| 3 | 120267 | Qtr2 | 15 |
| 4 | 120267 | Qtr3 | 15 |
| 5 | 120267 | Qtr4 | 15 |
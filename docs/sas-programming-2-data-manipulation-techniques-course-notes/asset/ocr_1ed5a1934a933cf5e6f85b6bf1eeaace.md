# Compilation: What Variables Are Created

```
data compare(drop=i Goal1-Goal4);
set orion.employee donations;
array Contrib{4} Qtr1-Qtr4;
array Diff{4};
array Goal{4} (10,20,20,15);
do i=1 to 4
  Diff{i}=Contrib{i}-Goal{i};
end;
```

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 | Diff1 |
|---|---|---|---|---||}{
| Diff2 | Diff3 | Diff4 | | | |

# Compilation: What Variables Are Created

```
data compare(drop=i Goal1-Goal4);
set orion.employee donations;
array Contrib{4} Qtr1-Qtr4;
array Diff{4};
array Goal{4} (10,20,20,15);
do i=1 to 4
  Diff{i}=Contrib{i}-Goal{i};
end;
```

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 | Diff1 |
|---|---|---|---|---|---||}{
| Diff2 | Diff3 | Diff4 | Goal1 | Goal2 | Goal3 | Goal4 |
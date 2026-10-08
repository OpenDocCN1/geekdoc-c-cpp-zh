# 7.08 Short Answer Poll

How many ARRAY statements would you use to calculate the difference in each employee's contribution from quarter to the next?

Partial orion.employee_donations

| Employee_ID | Qtr1 | Qtr2 | Qtr3 | Qtr4 |
|---|---|---|---|--|
| 120265 | | | | 25 |
| 120267 | 15 | 15 | 15 | |
| 120269 | 20 | 20 | 20 | |

> First difference: Qtr2 - Qtr1
Second difference: Qtr3 - Qtr2
Third difference: Qtr4 - Qtr3

# Creating Variables with Arrays

```
data change;
set orion.employee_donations;
drop l1;
array Contrib(4) Qtr1-Qtr4;
array Diff{3};
doi i=1 to 3;
Diff{i}=Contrib{i+1}-Contrib{i};
end;
```

The Contrib array refers to existing variables. The Diff array creates three variables: Diff1, Diff2, and Diff3.
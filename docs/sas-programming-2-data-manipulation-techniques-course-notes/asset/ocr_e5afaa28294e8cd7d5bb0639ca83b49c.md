# Summarizing Data by Groups

**Step 3** Output

| Dept | Salary | DeptSal |
|---|---|--|
| ADMIN | 20000 | 20000 |
| ADMIN | 100000 | 120000 |
| ADMIN | 50000 | 170000 |
| ENGINR | 25000 | 25000 |
| ENGINR | 20000 | 45000 |
| ENGINR | 23000 | 68000 |
| ENGINR | 27000 | 95000 |
| FINANC | 10000 | 10000 |
| FINANC | 12000 | 22000 |

# Summarizing Data by Groups

**Step 3** Output

```
data deptsals(keep=Dept DeptSal);
set SalSort;
by Dept;
if First.Dept then DeptSal=0;
DeptSal+Salary;
if Last.Dept; gone as if last.dept=1 then output,
run;
```

The subsetting IF defines a condition that the observation must meet to be further processed by the DATA step.
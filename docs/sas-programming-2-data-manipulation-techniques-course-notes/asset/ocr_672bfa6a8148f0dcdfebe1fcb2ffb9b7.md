# Creating Variables with Arrays

```
data change;
  set orion.employee_donations;
  drop i;
  array Contrib{4} Qtr1-Qtr4;
  array Diff{3};
  do i=1 to 3;
    Diff{i}=Contrib{i+1}-Contrib{i};
run;
```

```
when i=1
  Diff{1}=Contrib{2}-Contrib{1};
  Diff1=Qtr2-Qtr1;
```

# Creating Variables with Arrays

```
data change;
  set orion.employee_donations;
  drop i;
  array Contrib{4} Qtr1-Qtr4;
  array Diff{3};
  do i=1 to 3;
    Diff{i}=Contrib{i+1}-Contrib{i};
run;
```

```
when i=2
  Diff{2}=Contrib{3}-Contrib{2};
  Diff2=Qtr3-Qtr2;
```
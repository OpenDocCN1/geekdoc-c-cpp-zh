# 7.04 Short Answer Poll – Correct Answer

How can you generate the same result with a DO WHILE statement? Change the DO UNTIL statement to a DO WHILE statement and modify the condition.

```
data invest;
do while(Capital<=1000000);
  Year+1;
  Capital+5000;
  Capital+(Capital*.045);
end;

run;

proc print data=invest noobs;
  format capital dollar14.2;
run;
```

![](bbox=[0.608, 0.385, 0.668, 0.396])

# 7.05 Short Answer Poll – Correct Answer

How can you generate one observation for each quarterly amount? Move the OUTPUT statement to the inner loop and do not drop Quarter.

```
data invest;
do Year=1 to 5;
  Capital+5000;
  do Quarter=1 to 4;
    Capital+(Capital*(.045/4));
    output;
  end;
end;
```

| Year | Capital | Quarter |
|---|---|--|
| 1 | 5056.25 | 1 |
| 1 | 5113.13 | 2 |
| 1 | 5170.66 | 3 |
| 1 | 5228.83 | 4 |
| 2 | 10385.00 | 1 |
| 2 | 10460.27 | 2 |

```
proc print data=invest
run;
```

![](bbox=[0.618, 0.718, 0.678, 0.729])
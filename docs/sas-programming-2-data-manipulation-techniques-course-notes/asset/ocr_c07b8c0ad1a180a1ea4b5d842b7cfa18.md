# 7.1 DO Loop Processing 7-11

# Execution: Performing Repetitive Calculations

```
data invest;
do Year=2008 to 2010;
  Capital+5000;
  Capital+(Capital* .045);
end;
run;
```

![](bbox=[0.435, 0.245, 0.565, 0.265])

| Year | Capital | N |
|---|---|--|
| 2009 | 10225 | 1 |

20

# Execution: Performing Repetitive Calculations

```
data invest;
do Year=2008 to 2010;
  Capital+5000;
  Capital+(Capital* .045);
end;
run;
```

![](bbox=[0.415, 0.585, 0.615, 0.605])

| Year | Capital | N |
|---|---|--|
| 2009 | 10685.13 | 1 |

21

Copyright © 2014, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED.
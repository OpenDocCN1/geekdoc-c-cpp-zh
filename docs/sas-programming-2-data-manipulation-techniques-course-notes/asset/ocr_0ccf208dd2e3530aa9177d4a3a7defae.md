# Execution: Performing Repetitive Calculations

```
data invest;
do Year=2008 to 2010;
  Capital+=5000;
  Capital+(Capital*.045);
end;
```

![](bbox=[0.114, 0.237, 0.633, 0.323])

# Execution: Performing Repetitive Calculations

```
data invest;
do Year=2008 to 2010;
  Capital+=5000;
  Capital+(Capital*.045);
end;
```

![](bbox=[0.503, 0.483, 0.613, 0.558])

| Year | Capital | N |
|---|---|---|
| 2010 | 10685.13 | 1 |
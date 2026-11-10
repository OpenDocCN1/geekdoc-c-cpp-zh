# **TABLE 5.2:** Results for Analog Data

| Training Vectors | Test Vectors | Time (Secs) | Efficiency (%) |
|---:|---:|---:|---:|
| 20 | 80 | 2.01 | 51.56 |
| 40 | 60 | 3.98 | 73.95 |
| 60 | 40 | 5.78 | 89.06 |
| 80 | 20 | 9.23 | 93.75 |
| 95 | 5 | 9.36 | 100 |

```
```matlab
for i = 1:m1
    d(i) = sum(power((w(i,:)-
             data(1,:)),2));
end
[mind mini] = min(d);
output(p) = mini;
if(mini==value(p))
      count = count+1;
end
end

% RESULTS:
fprintf('\nPercentage of TRAING Vectors : % f',per1);
fprintf('\nPercentage of TEST Vectors : % f',per2);
fprintf('\nTime Taken for TRAINING : % f in secs',t);

eff = count*100/patterntest;
fprintf('\nEfficiency = % f',eff);
```
```

# **Observations:**

Tables 5.2 and 5.3 and show the results of KOHONEN for analog and digital inputs with optimum efficiency. It can be inferred that the efficiency increases with number of training vectors.

# **TABLE 5.3:** Results for Digital Data

| Training Vectors | Test Vectors | Time (Secs) | Efficiency (%) |
|---:|---:|---:|---:|
| 20 | 80 | 1.98 | 70.31 |
| 40 | 60 | 3.87 | 79.16 |
| 60 | 40 | 6.03 | 82.81 |
| 80 | 20 | 7.76 | 84.37 |
| 95 | 5 | 9.29 | 100 |
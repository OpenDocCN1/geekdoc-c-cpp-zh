# Performance Measuring

# **Algorithm 10** Program.progc

```
1: #include <stdio.h>
2: #include <math.h>
3: double new func1(double x)
4: {
5:
6:     int i = 0;
7:     double a[20000];
8:     printf("%n Inside func1 \n");
9:     for(i=0;i<20000;i++) {
10:         a[i] = i*sin(x);
11:    }
12:    return x;
13: }
```

More specifically, the **flat profile** has the following fields:

+   * **time** is the percentage of the total execution time the program spent in this function. These should all add up to 100%.
* **cumulative seconds** is the cumulative total number of seconds computer spent executing this function, plus the time spent in all the functions above this one in this table.
* **self seconds** is the number of seconds accounted for by this function alone. The flat profile listing is sorted first by this number.
* **calls** is the total number of times the function was called. If the function was never called, or the number of times it called cannot be determined, the calls field is blank.
* **self ms/call** represents the average number of milliseconds spent in this function per call if this is profiled.
* **total ms/call** represents the average number of milliseconds spent in this function and its children per call, if the function could not be profiled.
* **name** is the name of the function.

Before the column headers, a statement is shown indicating the sampling period ($T_s$). A estimate ($T_e$) that is not much larger than the sampling period is not reliable since $ns = T_e/T_s$ is small ($ns$ is the number of samples).

The call graph shows the time spent in each function and its children. It also displays, for each function, its function's callers, which functions are called by it, and how many times. There is also an estimate of the time spent in the children's functions of each function. Hence, such data can suggest places where we might optimize the code.
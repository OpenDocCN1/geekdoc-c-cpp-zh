
## 372 Performance, Reliability, Availability Evaluation of Computational Systems

## Algorithm 9 Program prog_m.c

```c
1: #include <stdio.h>
2: #include <math.h>
3: double new_func1(double x)
4: 
5: double func1(double x)
6: {
7:     double b[10000];
8:     int i = 0;
9:     printf("\n Inside func1\n");
10:    for(i=0;i<10000;i++)
11:        b[i] = i*pow(x,3);
12:        x = x + b[i];
13:    }
14:    x = new_func1(x);
15:    return x;
16: }
17: static double func2(double x)
18: {
19:     double c[10000];
20:     double d;
21:     int i = 0;
22:     printf("\nInside func2\n");
23:     for(i=0;i<6000;i++)
24:        c[i] = i*sqrt(x);
25:        x = x + c[i];
26:    }
27: 
28:     d = new_func1(x);
29:     return d;
30: }
31: int main(void)
32: {
33:     int i = 0, j = 0;
34:     double x[15000];
35:     double z[50000];
36:     printf("\nInside main()\n");
37:     for(i=0;i<5000;i++)
38:        x[j] = j*sqrt(i);
39:        j++;
40:        x[j] = func1(x[j-1]);
41:        j++;
42:        x[j] = func2(x[j-1]);
43:        z[i] = x[j-2]*x[j-1];
44:        j++;
45:     }
46:     for(i=0;i<5000;i++)
47:        z[i] = z[i] * z[i];
48:     return 0;
49: }
```

## Performance Measuring

## **Algorithm 10** Program.prog

```c
1: #include <stdio.h>
2: #include <math.h>
3: double new_func1(double x)
4: {
5: 
6:     int i = 0;
7:     double a[20000];
8:     printf("\n Inside func1 \n");
9:     for(i=0;i<20000;i++) {
10:         a[i] = i*sin(x);
11:    }
12:    return x;
13: }
```

More specifically, the **flat profile** has the following fields:

- **time** is the percentage of the total execution time the program spent in this function. These should all add up to 100%.
- **cumulative seconds** is the cumulative total number of seconds computer spent executing this function, plus the time spent in all the functions above this one in this table.
- **self seconds** is the number of seconds accounted for by this function alone. The flat profile listing is sorted first by this number.
- **calls** is the total number of times the function was called. If the function was never called, or the number of times it called cannot be determined, the calls field is blank.
- **self ms/call** represents the average number of milliseconds spent in this function per call if this is profiled.
- **total ms/call** represents the average number of milliseconds spent in this function and its children per call, if the function could not be profiled.
- **name** is the name of the function.

Before the column headers, a statement is shown indicating the sampling period ($T_s$). An estimate ($T_e$) that is not much larger than the sampling period is not reliable since $ns = T_e/T_s$ is small ($ns$ is the number of samples).

The call graph shows the time spent in each function and its children. It also displays, for each function, its function's callers, which functions are called by it, and how many times. There is also an estimate of the time spent in the children's functions of each function. Hence, such data can suggest places where we might optimize the code.

## 374 Performance, Reliability, and Availability Evaluation of Computational Systems

The lines full of dashes divide the data into entries, where each entry represents each function. Each entry has one or more lines. In each entry, the primary line is the one that starts with an index number in square brackets. At the end of this line, the function assigned to this entry is depicted. The preceding lines of the primary line of the entry describe the callers of this function. The following lines of the primary line of the entry describe its children's functions. The entries are sorted by time spent in function and its children's functions.

For profiling C program depicted in Program List 9 and 10, execute the command

```bash
> gcc -Wall -pg cfl.c cfl_n.c -o cfl -lm
```

After run, execute the code to generate the gmon.out. Then, execute the gprof to analyze the file gmon.out and display the profiling information on the file program_analysis.txt.

```bash
> gprof -b cfl gmon.out > cfl_analysis.txt
```

The flat profile obtained for the program

## Flat Profile

Flat profile:

Each sample counts as 0.01 seconds.

| cumulative seconds | seconds | calls | ms/call | name |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 73.24 | 75.30 | 75.30 | 5000 | 7.53 | new_func1 |
| 15.95 | 91.70 | 16.40 | 5000 | 3.28 | func1 |
| 10.80 | 102.80 | 11.10 | 5000 | 2.22 | func2 |
| 0.01 | 102.81 | 0.01 | | main |

The first information we obtain from the profile is the sampling period, $T_s = 0.01s$, where the profile states, "Each sample counts as 0.01 seconds.". Then, we have information related each function to the fields above. In this particular case, new_func1 is responsible for 73.24% of the execution of the whole program. The time spent on this function was 75.30. It is worth noting that the sampling period is much shorter than the time spent executing the function ($0.01s < 75.30s$), which suggests 75.30s as a reliable estimate. We also see that function $new\_func1$ was called 5000 times during the program execution, and the mean time spent by this function per call was 7.53ms. The second most demanding function was func1, which was responsible for 15.95% of the program's execution time, which demanded 16.40s in its execution without considering its functions. The time demanded up to 91.70s. This function was called 5000 times during

## Performance Measuring

the program execution, the mean time spent by executing func1 per call was 3.28ms. Likewise, func2 function was the third most demanding function and was responsible for 10.80% of the program's execution time. This function demanded 11.10s in execution without its children's functions. The function func2 was called 5000 times during the program execution, and the mean time spent by this function was 2.22ms. The program's execution time estimate was 102.81s and is obtained from the cumulative line. The second part of the profile is the call graph. It depicts the time spent in each function and its children. Moreover, call graph also displays the callers of each function, function graph each function, and the number of function's calls. Moreover, an estimate of the time spent in the children's functions of each function is also provided.

## Call Graph

granularity: each sample hits (s) for 0.01% of 102.81 seconds

| Index by function | % time | self | children | name |
| :--- | :--- | :--- | :--- | :--- |
| --- | --- | --- | --- | --- |
| [1] | 100.0 | 0.01 | 102.81 | 5000/5000 main |
| [2] | 73.24 | 73.30 | 75.30 | 5000/10000 new_func1 |
| [3] | 15.95 | 16.40 | 91.70 | 5000/5000 func1 |
| [4] | 10.80 | 11.10 | 102.80 | 5000/5000 func2 |

The first entry of the call graph is [1], which is related to main. The previous line shows is not called by any other function (see the keyword "spontaneous"). The main function calls func1 and func2. This is shown in the two consequent lines of the primary line. The time spent in the main function itself denoted to the execution of function func1 was 16.40s. Similarly, the time spent in the main function related to the execution of function func2 was 11.10s. The time spent when

## 376 Performance, Reliability, and Availability Evaluation of Computational Systems

executing each of these children's function was equal to 37.65s for func1 and func2, respectively. Adding up 16.40s, 11.10s, and 2 × 37.65s totaled 102.80, which was the execution time estimate. The second entry of the call graph is [2]. This entry focuses on new_func1 and func2. The preceding lines of the primary line of this entry inform the functions that call new_func1. Therefore, we have func1 and func2. The time spent executing new_func1 due to function calls was 37.65s. Likewise, the time spent executing new_func2 to func2 was 37.5s. Hence, summing up, we obtain 75.30s. The time spent by new_func1 children's functions was null. Entry, new_func has no child. Function calls calls new_func1 5000 times of a total of 10000. Similarly, function func2 calls new_func1 5000 out of 10000. Hence, no function other than func1 and func2 calls new_func1. The third entry of the call graph is [3], which analyzes func1. Function func1 is called only by the main function. The time spent executing func1 itself was 36.40s, and the time spent its children functions was 37.65s. Function func1 was called 5000 times and also called new_func1 5000 times. As we already seen, new_func1 is called 10000 times. The last entry of the call graph is [4], which analyzes function func2. Function func2 is called only by the main function, and the time spent executing function func2 itself was 11.10s and the time spent executing its children functions was 37.65s. Function func2 was called 5000 times and also called new_func1 5000 times.

## 23.7 COUNTERS AND BASIC PERFORMANCE TOOLS IN LINUX

The aim of this section is not to reference Linux counters and performance monitoring tools. The goal is to introduce some features and point out specific references in-depth. The operating systems (OS) documentation is the best source to find out how you can collect performance metrics through its performance counters [443, 470]. The system performance measures are accessible to programmers via call services (syscalls - mostly with Int 80h for Intel-based Unix system), which services are implemented in the Linux kernel [51, 113, 141, 306, 382, 397, 422]. When a program makes a system call, the arguments are handled by the kernel, which takes over the program's execution until the respective call finishes.

Linux provides a virtual filesystem /proc, also called a proc-filesystem, which contains a rich source of information about the hardware, kernel, and processes running on the system. It appears to the user as a common filesystem such as /home. The /proc virtual filesystem can be used with well-known Linux commands and tools such as cat, more, grep, open, read, write, awk, printf, echo, cron that also be used in monitoring scripts.

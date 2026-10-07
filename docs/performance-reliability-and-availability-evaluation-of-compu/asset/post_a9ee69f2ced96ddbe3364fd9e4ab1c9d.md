
## Table 23.3
Server Utilization - Sample Frequency = 2 samples/min

| Utilization - $U_i$ | | | |
|---|---|---|
| 0.44 | 0.34 | 0.62 |
| 0.70 | 0.58 | 0.70 |
| 0.56 | 0.68 | 0.61 |
| 0.40 | 0.40 | 0.67 |
| 0.43 | 0.63 | 0.44 |
| 0.49 | 0.44 | 0.62 |
| 0.46 | 0.31 | 0.68 |
| 0.43 | 0.65 | 0.53 |
| 0.44 | 0.65 | 0.39 |
| 0.48 | 0.69 | 0.34 |

## Table 23.4
Servers' Utilization Sample - Sample Frequency = 0.5 samples/s

| $U_{S1}$ | | $U_{S2}$ | | | |
|---|---|---|---|---|---|
| 0.36 | 0.38 | 0.62 | 0.41 | 0.70 |
| 0.41 | 0.38 | 0.35 | 0.61 | 0.66 | 0.50 |
| 0.30 | 0.30 | 0.41 | 0.73 | 0.74 | 0.66 |
| 0.32 | 0.39 | 0.41 | 0.58 | 0.50 | 0.40 |
| 0.30 | 0.39 | 0.40 | 0.46 | 0.40 | 0.68 |

utilization measures of each server are presented in Table 23.4. The IO operation takes, on average, 50ms.

- (a) What is the average time a transaction demands from each server and the storage system?
- (b) Which component is the system bottleneck?

**Exercise 15.** Consider a C language program source that multiplies two $8 \times 8$ matrices and calculates the time required to multiply them by inserting function calls inside the source code.

**Exercise 16.** Using a programming language of choice and implement a program that calculates the inverse of a matrix of $8 \times 8$. Insert time function calls inside the source code to calculate the time required to obtain the matrix inversion.

**Exercise 17.** Explain why and how the time measurement system overhead may be a restraint for adopting an event measuring strategy to quantify the events' duration.

## 434 Performance, Reliability, Availability Evaluation of Computational Systems

**Exercise 18.** Would the statistical measurement-based strategy be an alternative for measuring short-duration events? What are the pros and cons of methods based on this strategy? Comment.

**Exercise 19.** Consider a computer program composed of many functions (methods or routines), and assume the expected time to process a specific function, named $f_1$, is very short. In other words, the execution time of this function is about the same order (or shorter) as the smallest duration the direct measurement mechanism supported by the computer can quantify. The *instruction-pointer sampling* strategy is adopted to estimate the execution time of function $f_1$.

Let us consider that the interruption frequency is $10kHz$, and assume the system (program running on the computer) was monitored for $8h$. Then, from the total number of samples, $1,679,623$ addresses belong to the address range of function $f_1$.

- (a) Obtain the point estimate of the time to execute $f_1$.
- (b) Considering a degree of confidence of $95\%$, calculate the confidence interval of the time to execute $f_1$ by considering that the normal distribution approximates the binomial distribution.

**Exercise 20.** What is a deterministic profile? Explain.

**Exercise 21.** What is a statistical profile? Explain.

**Exercise 22.** What are the pros and cons of deterministic and statistical profiling strategies? Explain each characteristic.

**Exercise 23.** Use *gprof* to evaluate the C language code depicted in List 11. This program generates 1000 lists of 25 prime numbers. Each prime number is in the range $0 - 10000$. For each, each list, the largest prime is also shown.

- (a) Present the flat, the graph profiles, and interpret them.
- (b) Adjust the code by adopting suitable programming practices for improving its performance. Check the performance of the new version of the program by using *gprof*.

**Exercise 24.** Use a programming language of choice (different from C programming language) and implement the same functionality described by the program depicted in Exercise 23. In addition, use a profiling tool that supports the programming language.

- (a) Generate a program profile and analyze the program’s most demanding function (routines, methods, procedures, etc.).
- (b) Adjust the original code for improving its performance.

## Performance Measuring

### Algorithm 11 C Program - Exercise 23

```c
#include <sysime.h>
#include <stdio.h>
#include <stdlib.h>
int *mrat(int al2, int mn) {
    struct timeval tv;
    gettimeday(&tv,NULL);
    int *as = 0;
    int i;
    as = (int*)malloc(al2*sizeof(int));
    for(i=0; i<al2; i++)
        as[i] = (random() % mn) + 2;
    return as;
}
int ip(int x) {
    int y;
    for(y=2; y<x; y++)
        if(x % y == 0)
        return 1;
    return 0;
}
int *fp(int al3, int arr[]) {
    int *as = 0;
    int i;
    as = (int*)malloc(al3*sizeof(int));
    for(i=0; i<al3; i++)
        if(ip(arr[i]))
        as[i] = 1;
    return as;
}
int fl(int al4, int *nums, int *ips) {
    if(al4<=0)
        return NULL;
    if(ips[al4-1])
        return fl(al4-1, nums, ips);
    return nums[al4-1];
}
void vp(int al5, int *nums, int *ips, int l1) {
    int i;
    for(i=0; i<al5; i++)
    if(ips[i])
        printf("%d\tThe largest prime is %d\n", nums[i], l1);
}
int main() {
    int i, l1, al1, mn1;
    int *ra = 0;
    int *pr = 0;
    int k = 1000;
    al1 = 25;
    al2 = 10000;
    mn1 = 1000;
    printf("Generate %d list(s) of size %d of primes - Each prime is 0 to %d\n", mn1, al1, al2);
    for(i=0; i<k; i++) {
        al = al1;
        mn = mn1;
        ra = mrat(al, mn);
        pr = fp(al, ra);
        l = fl(al, pr);
        printf("List number %d\t%d\n", l, i);
        free(ra);
        free(pr);
    }
    return 0;
}
```

## 436 Performance, Reliability, and Availability Evaluation of Computational Systems

**Exercise 25.** For a computer system with a Linux operating system, obtain the contents of the following entries and interpret them:

- (a) /proc/cpuinfo carries data specifying processors and system architecture.
- (b) /proc/meminfo holds statistics on memory usage.
- (c) /proc/stat contains processors and memory usage information.
- (d) /proc/uptime carries the idle duration since the boot.
- (e) /proc/devices defines the character and block devices currently configured.
- (f) /proc/diskstat holds the I/O statistics of block devices.
- (g) /proc/iomem holds the current map of the system’s memory for each physical device.
- (h) /proc/ports contains a list of currently registered ports for input or output communication with a device.

**Exercise 26.** The Script 12 below collects one hundred-sized sample of memory utilization using the command `free`. The delay between measures is sixty seconds. At each collect, capture the total memory used and the free memory in megabytes. The script produces a file organized in columns.

### Algorithm 12 Memory Collection Script - Exercise 26

```bash
free -m | awk 'NR=1{printf "%s %s\n", $2, $3}' >> memfree.txt;
for i in (1..100)
do
  free -m | awk 'NR=2{printf "%d %d\n", $2, $3}' >> memfree.txt;
  sleep 60
done
```

- (a) Write a short document defining the computer system’s current state by specifying the computer model, the number of processors, the operating system, the applications under execution, and the performance policy, and execute Script 12.
- (b) Provide a statistical summary for the collected sample and suitable graphs to support the data analysis.
- (c) Write a textual summary describing and interpreting measured data.
- (d) Use dstat to collect the sample instead of the script above.
- (e) Comment on the pros and cons of adopting dstat.

**Exercise 27.** Script 13 collects one hundred-sized sample of CPU utilization through command top. The delay between measures is one hundred and twenty seconds. At each collect, capture the CPU utilization in each specific state: *us, sy, ni, wa, hi, and st.* The script produces a txt file organized in columns.

### Algorithm 13 CPU Utilization Considering the State Classes - Collection Script - Exercise 27

```bash
top -b n 1 | awk 'NR=3{printf "%s %s %s %s %s %s %s %s\n", $3, $5, $7, $9, $11, $13, $15, $17}' >> topcpu.txt;
for i in (1..100)
do
  top -b n 1 | awk 'NR=3{printf "%.2f%% %.2f%% %.2f%% %.2f%% %.2f%% %.2f%% %.2f%% %.2f%%\n", $2/100, $4/100, $6/100, $8/100, $10/100, $12/100, $14/100, $16/100}' >> topcpu.txt;
  sleep 120;
done
```

- (a) Write a short document defining the computer system’s current state by specifying the computer model, the number of processors, the operating system, the applications under execution, and the performance policy, and execute Script 13.
- (b) Analyze the sample and provide its statistical summary and suitable graphs to represent the collected data.
- (c) Write a summary describing and interpreting the sample and the possible features of the system.
- (d) Use dstat to collect the sample instead of the script above.
- (e) Comment on the pros and cons of adopting dstat.

**Exercise 28.** Through command top. Script 14 collects one hundred-sized sample of CPU utilization. The delay between measures is sixty seconds. The script produces a txt file organized in columns.

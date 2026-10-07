
## Workload Characterization

gettimeofday(&end, 0);

The execution time was, then calculated by

```c
long seconds = end.tv_sec - begin.tv_sec;
long microseconds = end.tv_usec - begin.tv_usec;
double elapsed = seconds + microseconds*1e-6;
```

The command if (finisec-startsec <= 0) was substituted by

```c
if (elapsed <= 0)
```

and the command lines

```c
printf("Loops: %ld, Iterations: %d, Duration: %ld sec.\n",
LOOP, II, finisec-startsec);
KIPS = (100.0*LOOP+II)/(float) (finisec-startsec);
```

were also changed to

```c
printf("Loops: %ld, Iterations: %d, Duration: %.3f sec.\n",
LOOP, II, elapsed);
KIPS = (100.0*LOOP+II)/(float) elapsed);
```

Finally, the command line

```c
printf("C Converted Double Precision Whetstones: %.1f MIPS\n",
KIPS/1000.0);
```

was also substituted to

```c
printf("C Converted Double Precision Whetstones: %.3f KIPS\n",
KIPS);
```

An script (scriptwstone) was also implemented to execute the benchmark n (in the case below n = 100). The script lines are

```bash
scriptwstone
```

```bash
printf "Whetstone Results \n" >> whetstone_result.txt;
for i in {1..100}
do
whetstone >> whetstone_result.txt;
done
```

## Performance, Reliability, and Availability Evaluation of Computational Systems

Table 24.1
Whetstone Execution Time (s)

| Sample - Sample Size = 100 |
| :--- |
| 5.938 | 5.198 | 5.188 | 5.424 | 8.751 | 5.165 | 5.811 | 5.195 | 5.141 | 5.241 | 5.236 |
| 6.19 | 6.005 | 5.202 | 5.158 | 5.311 | 5.224 | 5.676 | 5.444 | 5.141 | | |
| 5.535 | 6.024 | 5.216 | 5.385 | 5.272 | 5.35 | 5.378 | 5.262 | 5.244 | 5.238 |
| 5.564 | 5.372 | 5.206 | 5.273 | 5.231 | 5.206 | 5.419 | 5.469 | 5.202 | 5.204 |
| 5.289 | 5.175 | 5.467 | 5.314 | 5.239 | 5.382 | 5.172 | 5.905 | 5.195 | 5.149 |
| 6.098 | 5.157 | 5.44 | 5.314 | 5.283 | 5.35 | 5.278 | 6.48 | 5.854 | 5.173 |
| 5.53 | 5.379 | 5.183 | 5.414 | 5.211 | 5.29 | 5.239 | 5.239 | 5.314 |
| 5.407 | 5.522 | 5.151 | 5.569 | 5.181 | 5.864 | 5.124 | 5.108 | 5.337 | 5.569 |
| 5.486 | 5.231 | 5.211 | 5.514 | 5.564 | 5.595 | 5.102 | 5.108 | 5.225 | 5.736 |
| 5.431 | 5.258 | 5.383 | 5.741 | 5.51 | 5.184 | 5.094 | 5.275 | 5.256 |

Table 24.2
Whetstone - MIPS

| Sample - Sample Size = 100 |
| :--- |
| 1683.996 | 1923.607 | 1927.685 | 1843.668 | 1142.7 | 1936.192 | 1720.965 | 1925.104 | 1950.059 | 2009.686 |
| 1615.527 | 1665.152 | 1971.106 | 1917.112 | 1835.776 | 1982.938 | 1948.238 | 1761.684 | 1939.361 | 1901.436 |
| 2009.291 | 1866.663 | 1932.305 | 1829.229 | 1805.472 | 1817.076 | 1886.058 | 1948.283 | 1933.662 | 1924.819 |
| 1942.138 | 1797.136 | 1861.357 | 1920.785 | 1908.317 | 1886.819 | 1918.858 | 1934.924 | 1845.486 | 1770.243 |
| 1922.518 | 1921.67 | 1890.841 | 1932.305 | 1829.209 | 1881.819 | 1982.963 | 1918.858 | 1938.556 | 1918.856 |
| 1962.693 | 1958.487 | 1942.138 | 1639.119 | 1939.992 | 1834.246 | 1881.111 | 1836.089 | 1869.048 | 1924.629 |
| 1913.526 | 1708.142 | 1932.928 | 1808.351 | 1859.077 | 1929.354 | 1941.507 | 1847.106 | 1919.114 | 1980.382 |
| 1935.436 | 1908.789 | 1814.831 | 1785.765 | 1849.329 | 1915.63 | 1941.507 | 1795.694 | 1929.763 | 1705.451 |
| 1951.618 | 1959.191 | 1873.534 | 1795.563 | 1822.206 | 1911.543 | 1942.119 | 1813.725 | 1792.792 | 1787.359 |
| 1960.713 | 1963.905 | 1974.328 | 1742.325 | 1843.381 | 1901.907 | 1857.621 | 1841.785 | 1815.013 | 1985.035 |
| 1924.094 | 1962.944 | 1985.725 | 1902.761 | 1806.269 |

such that whetstone_result.txt file the execution times and iterations per each execution were stored. This experiment was executed in a small Linux virtual machine deployed as a personal computer. Table 24.1 depicts execution times (s) and Table 24.2 shows the respective MIPs.

The statistical summary for the execution time and MIPs is shown in Table 24.3. The confidence interval, the mean execution time (s), and the average MIPs (MIPS) with 95% degree of confidence were calculated using the nonparametric bootstrap procedure: (5.3405, 1165).

## Table 24.3 Whetstone Statistical Summary - Execution Times and MIPs

| Execution Times (s) | MIPs |
| :--- | :--- |
| Mean (s) | 5.1435 | Mean (MIPs) | 1950.005 |
| SD (s) | 0.1412 | SD (MIPs) | 119.6115 |
| Variance (s²) | 0.0199 | Variance (MIPs²) | 1430.9025 |
| CoV (%) | 2.7444 | CoV (%) | 6.1339 |
| Q1 (s) | 5.0523 | |
| Median (s) | 5.0845 | |
| Q3 (s) | 5.1928 | |
| Minimal (s) | 5.1405 | Minimal (MIPs) | 1666.7 |
| Maximal (s) | 5.944 | Maximal (MIPs) | 2000 |
| Range (s) | 0.949 | Range (MIPs) | 333.3 |
| Skewness | 2.5927 | Skewness | -1.990374 |
| Kurtosis | 10.1346 | Kurtosis | 2.0012 |

respectively. (1830.7399 MIPS, 1874.2690 MIPS).

## Linpack

The original LINPACK Benchmark was, in some sense, an accident since it was initially designed to support Linpack package users by providing information on the execution times required to solve system of linear equations. The first version of Linpack Benchmark appeared as an appendix in Linpack Users' Guide in 1979. Results were provided for matrix problem of size 100 on collection of widely used computers. This was done so users could estimate the time required to solve matrix problems by extrapolation. Its performance is represented in FLOPS (GFLOPS, TFLOPS). Over the years, additional performance data was added, and the collection includes a vast number of computer systems. Besides, the scope of the benchmark has also expanded. The original version was produced in Fortran, but a C programming version appeared later. Nowadays, there are many variants and extensions of Linpack. For instance, the Optimized Linpack Benchmark for Linux is a generalization of the Linpack 1000 Benchmark, which handles matrices of order 100. It calculates dense linear equations, estimates the time it takes to solve the system, converts that time into a performance rate, and tests its accuracy. It is worth highlighting that the number of equations (N) is not limited to 1000 as some previous versions.

## Performance, Reliability, and Availability Evaluation of Computational Systems

As an example, we adopted the LinpackBENCH, which is a C program that drives the single and double precision Linpack benchmark program (see Appendix C). The source adopted here embodies both single and double precision specified at compilation time. Furthermore, we may also use a compiler option to allow “rolled loops” (default) or “unrolled loops”.

We included the library sys/time.h for improving the measurement system's precision. Thus, we added the following line.

```c
#include <sys/time.h>
```

and two structure variables were declared with structures timeval:

```c
struct timeval begin, end;
```

The command for starting measuring the execution time was substituted to

```c
gettimeofday(&begin, 0);
```

and the command for getting the instant at the end of the piece of code we intend to measure was also substituted to

```c
gettimeofday(&end, 0);
```

The execution time was, calculated by

```c
long seconds = end.tv_sec - begin.tv_sec;
long microseconds = end.tv_usec - begin.tv_usec;
double elapsed = seconds + microseconds*1e-6;
printf("Time measured: %.3f seconds.\n", elapsed);
```

Hence a macro-view of the C code main function is shown below.

```c
struct timeval begin, end;

int main () {
    // Start measuring time
    // gettimeofday(&begin, 0);

    // Stop measuring time and calculate
```

```c
// the elapsed time

gettimeofday(&end, 0);
long seconds = end.tv_sec - begin.tv_sec;
long microseconds = end.tv_usec - begin.tv_usec;
double elapsed = seconds + microseconds*1e-6;
printf("Duration: %.3f sec.\n \n",elapsed);
return 0;
```

where the execution time of the Linpack executable is registered in variable elapsed and displayed on the screen as it "Duration". The script file depicted later redirects output to the text file "Linpack.result.txt". Besides, the three pieces of code below were commented. They are:

# Piece of Code 1

# Piece of Code 2

and

# Piece of Code 3

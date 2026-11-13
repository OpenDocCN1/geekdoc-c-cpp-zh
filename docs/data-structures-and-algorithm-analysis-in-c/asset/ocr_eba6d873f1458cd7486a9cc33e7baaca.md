| | $j_3$ | $j_2$ | $j_4$ | $j_1$ |
|---|---|---|---|---|
| 0 | 3 | 11 | 21 | 36 |

# Figure 10.3 Schedule #2 (optimal)

(time units). $j_2$ in 23, $j_3$ in 26, and $j_4$ in 36, the average completion time is 25. A better schedule, which yields a mean completion time of 17.75, is shown in Figure 10.3.

The schedule given in Figure 10.3 is arranged by shortest job first. We can show that this will always yield an optimal schedule. Let the jobs in the schedule be $j_1, j_2, \dots, j_N$. The first job finishes in time $t_1$. The second job finishes after $t_1 + t_2$, and the third job finishes after $t_1 + t_2 + t_3$. From this, we see that the total cost, $C$, of the schedule is

```
$C = \sum_{k=1}^N (N - k + 1)t_k$ (10.1)
```

```
$C = (N + 1) \sum_{k=1}^N t_k - \sum_{k=1}^N k \cdot t_k$ (10.2)
```

Notice that in Equation (10.2), the first sum is independent of the job ordering, so only the second sum affects the total cost. Suppose that in an ordering there exists some $x > y$ such that $t_x < t_y$. Then a calculation shows that by swapping $j_x$ and $j_y$, the second sum increases, decreasing the total cost. Thus, any schedule of jobs in which the times are not monotonically nondecreasing must be suboptimal. The only schedules left are those in which the jobs are arranged by smallest running time first, breaking ties arbitrarily.

This result indicates the reason the operating system scheduler generally gives precedence to shorter jobs.

# Multiprocessor Case

We can extend this problem to the case of several processors. Again we have jobs $j_1, j_2, \dots, j_N$, with associated running times $t_1, t_2, \dots, t_N$, and a number $P$ of processors. We will assume without loss of generality that the jobs are ordered, shortest running time first. As an example, suppose $P = 3$, and the jobs are as shown in Figure 10.4.

Figure 10.5 shows an optimal arrangement to minimize mean completion time. Jobs $j_1, j_4$, and $j_7$ are run on Processor 1. Processor 2 handles $j_2, j_5$, and $j_8$, and Processor 3 runs the remaining jobs. The total time to completion is 165, for an average of $\frac{165}{3} = 18.33$.

The algorithm to solve the multiprocessor case is to start jobs in order, cycling through processors. It is not hard to show that no other ordering can do better, although if the number of processors, $P$, evenly divides the number of jobs, $N$, there are many optimal orderings. This is obtained by, for each $0 \le i < N/P$, placing each of the jobs $j_{iP+1}$ through $j_{(i+1)P}$ on a different processor. In our case, Figure 10.6 shows a second optimal solution.

Even if $P$ does not divide $N$ exactly, there can still be many optimal solutions, even if all the job times are distinct. We leave further investigation of this as an exercise.
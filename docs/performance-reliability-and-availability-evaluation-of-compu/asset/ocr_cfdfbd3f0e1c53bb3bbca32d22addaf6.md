# 356 Performance, Reliability, and Availability Evaluation of Computational Systems

```
Algorithm 1 Measuring the Duration of a Piece Of Code in a Program
1:
2:
3: Start_count = read_timer();
4:
5: Piece of code being measured
6:\...
7: Stop_count = read_timer();
8: Elapsed_time = (stop_count - start_count) × clock_period;
9:
10:
```

time). This function returns both the number of seconds and microseconds in separate double variables that to obtain the total time, including microseconds, we need to sum both together accordingly. The piece of code depicted in Program 3 shows how to calculate the duration of a function. In this particular example, the execution time of func() is measured. The command lines in red depict specific commands essential for estimating the execution time.

If fractions of seconds are not important, we can obtain the elapsed time by calculating end.tv_sec - begin.tv_sec. The second argument of gettimeofday() is to specify the current timezone. Since we are calculating the elapsed time, timezones is irrelevant, provided that the same value is used for both begin and end. Thus, we use zero for both calls.

Estimating the event duration (T_e) using such an approach, the result measure more than the event duration itself (see Figure 23.6). It is important to stress that accessing the timer requires memory reading operations and may require a call to the operating system kernel. Besides, the value read from the timer is stored as a variable, which requires memory writing execution. Such a process is executed twice. First, it is executed at the beginning of the event, which has the overhead T1 + T2, and then again at the end of the event, causing the overhead T3. These operations may add a significant amount of time (overhead) to the duration of the event itself.

> overhead = T1 + T2 + T3.

This overhead may be significant if overhead is the order of the event duration (ed). If overhead << T_e, overhead could be disregarded. However, if overhead ∞ T_e or overhead > T_e, these operations add up to a significant delay to the duration of the event; thus, it is not suitable to measure an event of such a time order. Section 23.7 provides a quick view of the Linux performance counters and basic tools.
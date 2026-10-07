# Performance Measuring

displays statistics on processes and resource usage, the second part shows a list of running processes. If “top” is executed, the first part of the report is similar to the one in the screenshot below.

```
top - 12:58:59 up 8:02, 1 user, load average: 0.01, 0.05, 0.01
Tasks: 228 total, 2 running, 226 sleeping, 0 stopped, 0 zombie
%Cpu: 0.7 us, 0.7 sy, 98.7 id, 0.0 wa, 0.0 hi, 0.0 st
KiB Mem: 206152 total, 734656 free, 701080 used, 625976 buff/cache
KiB Swap: 998396 total, 998396 free, 0 used, 1095722 avail
```

At the left of the screen, top displays the current time (12:58:59) in the format hh:mm, followed by the uptime expressed in hours and minutes, which tells us the system has been running. In this specific case, the system has been running only for eight minutes and two seconds. Next comes the number of active users. In example, there is only one active user session. Finally, the average load over-represents the processors’ utilization over the last minute, the last five minutes, and the last fifteen minutes, respectively. In example, over the last minute, the processors’ utilization was 1% on average. Similarly, over the last five minutes, the processors’ utilization was 5% on average. Likewise, over the last fifteen minutes, the processors’ utilization was 1% on average.

For multiple processes or multi-core systems, a load of caution is required. If one has a load of 1 on a single-processor (or single-core) computer, this means your processor (core) had utilization 100% over the period. If one has a load average of 2 on a single-processor computer, this means the computer was overloaded by 100%, that is (100% + 100%). On a computer with two processors, a load average of 2 denotes the two processors were 100% in use. Finally, on a system with four processors, a load average of 2 means that each processor has utilization of 50% over the entire period.

The second line shows the tasks statistics regarding the processes running on a system. The "total" value is simply the total number of processes. For example, in the above screenshot, there are 228 processes, where 2 are running and 226 are sleeping. The third line has the processor’s utilization details, where

+   * us : time running uniced user processes.
* sy : time running kernel processes.
* ni : nice time running niced user processes.
* id : time spent in the kernel idle handler.
* wa : IO-wait time waiting for I/O completion.
* hi : time spent servicing hardware interrupts.
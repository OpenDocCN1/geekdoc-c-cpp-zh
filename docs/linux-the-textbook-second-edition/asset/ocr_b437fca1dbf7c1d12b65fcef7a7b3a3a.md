**TABLE 10.7**

*Brief Description of Some of the Interactive Keystroke Commands of top*

| Command | Meaning |
|---|---|
| `H` | Display/toggle the threads statistics on separate lines |
| `S` | Display/toggle system processes |
| `^L` | Redraw screen |
| `h or ?` | Display summary of interactive keystrokes |
| `k` | Kill processes whose space-separated PID-list is specified |
| `n or #` | Change the number of processes to display |
| `o or O` | Other-filtering—You will be prompted for the selection criteria which then determines which tasks will be shown in the “current” window |
| `R` | Change the nice value of a list of processes specified as space-separated PIDs |
| `S` | Change periodic update time (in seconds) |
| `t` | Toggle the display of top process |
| `z` | Switches the “current” window between your last used color scheme and the older form of black-on-white. |

**TABLE 10.8**

*Default Fields of the Output of the top Command with Brief Descriptions*

| Field | Description |
|---|---|
| `%CPU` | CPU usage—The task’s share of the elapsed CPU time since the last screen update, expressed as a percentage of total CPU time |
| `%MEM` | Memory usage (RES)—A task’s currently used share of available physical memory |
| `COMMAND` | Command name or command line—Display the command line used to start a task or the name of the associated program |
| `NI` | Nice value—The nice value of the task. A negative nice value means higher priority, whereas a positive nice value means lower priority |
| `PID` | Process id—The task's unique PID, which periodically wraps, though never restarting at zero |
| `PR` | Priority—The scheduling priority of the task |
| `RES` | Resident memory size (KiB)—The nonswapped physical memory a task is using |
| `S` | Process status—The status of the task which can be one of the following: D = uninterruptible sleep, R = running, S = sleeping, T = stopped by job control signal, t = stopped by debugger during trace, Z = zombie |
| `SHR` | The amount of VIRT memory that is shareable |
| `TIME+` | CPU time, hundredths—The same as TIME, but reflecting more granularity through hundredths of a second |
| `USER` | User name—The effective user name of the task owner |
| `VIRT` | Virtual memory size (KiB)—The total amount of virtual memory used by the task. It includes all code, data, and shared libraries plus pages that have been swapped out and pages that have been mapped but not used |

```
```text
$ top
top - 21:17:44 up 82 days,  2:25,  3 users,  load average: 0.37, 0.28, 0.29
Tasks: 178 total,   1 running, 177 sleeping,   0 stopped,   0 zombie
%Cpu(s):  7.7 us,  0.2 sy,  0.0 ni, 92.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem :  8079236 total,  2255528 free,  231152 used,  5592556 buff/cache
KiB Swap:  8292348 total,  8206680 free,    8568 used.  7063932 avail Mem

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
24303 root      20   0  123204   7532   6392 S   0.7  0.1   0:00.06 shd
24302 sarwar    20   0   42116   3780   3160 R   0.3  0.0   0:00.04 top
    1 root      20   0  119836   4664   2976 S   0.0  0.1   1:42.38 systemd
    2 root      20   0       0      0      0 S   0.0  0.0   0:00.81 kthreadd
    3 root      20   0       0      0      0 S   0.0  0.0   0:13.36 ksoftirqd/0
    5 root       0 -20       0      0      0 S   0.0  0.0   0:00.00 kworker/0:+
    7 root      20   0       0      0      0 S   0.0  0.0 113:00.38 rcu_sched
```
```
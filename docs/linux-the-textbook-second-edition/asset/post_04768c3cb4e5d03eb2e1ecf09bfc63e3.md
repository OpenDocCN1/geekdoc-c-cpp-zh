
## TABLE 10.6

### Headers of the top Command for Linux Mint

```text
top - 14:07:29 up 30 days, 21:30, 1 user, load average: 0.50, 0.36, 0.31
Tasks: 250 total, 1 running, 248 sleeping, 0 stopped, 1 zombie
%Cpu(s): 7.0 us, 3.9 sy, 0.0 ni, 88.9 id, 0.0 wa, 0.0 hi, 0.2 si, 0.0 st
KiB Mem : 5981672 total, 833348 free, 975496 used, 4172828 buff/cache
KiB Swap: 6157308 total, 6155404 free, 1904 used. 4641868 avail Mem
```

Depends on the Linux variant on which the command runs. The information in the header can include load average, time (days+hours:minutes:seconds) the system has been up and running, current time, number of processes on the system, number of processes sleeping, number of zombie processes, CPU utilization (percentages of idle time, user time, kernel/system time, and interrupt-handling time), utilization of user area in the main memory (total and free), and swap space (total and free). Table 10.6 gives a listing of top command header information for Linux Mint.

Most of the features of the top command can be selected by an interactive keystroke command while top runs. The following syntax box gives common command line options, and Table 10.7 gives a brief description of the top command’s interactive keystrokes.

```text
Syntax:
  top [options]
Purpose: Display and periodically update information about processes currently running on the system
Output: The various attributes of processes currently running on the system, periodically updated
Commonly used options/features:
  -H    Display statistics for each thread of a multithreaded process, one line per thread
  -i    Do not display idle processes
  -p    Monitor only processes with specified PIDs.
  -S    Display/toggle system processes.
  -u username    Display statistics for only those processes belonging to username
  -o field    Sort display by field, a header of a column in output in lowercase—for example, cpu, pri, res, or time
  -s    Starts top with secure mode forced, even for root.
  -c    Display full command line for each process or just command name.
The options -H, -i, -p, -s, and -c are really toggles.
```

In the following text, we show example sessions of the top command output. The following is a run of the command without any options. The command output shows that the system has been up and running for 82 days without crashing. Further, 178 processes are currently in the system, with one running, 177 sleeping, and zero stopped or in the zombie state. The systemd process, owned by root, is PID 1. The rcu_sched process, PID 7, has used 112 h and 59.23 s of the CPU time that it and its dead children have used. You can appreciate other values in the header and attributes of the processes by using Table 10.8. If you observe the command output for a little while, you will notice that the processes move up and down as their priorities change. Similarly, the statistics in the header are also updated periodically. Also notice that PID 1 is listed as systemd, the program name of that process, not the path to the command. We can use the c interactive top command on our Linux Mint system to toggle the display of the COMMAND column to show the paths to the commands that execute the processes.

## TABLE 10.7

### Brief Description of Some of the Interactive Keystroke Commands of top

| Command | Meaning |
|---|---|
| `H` | Display/toggle the threads statistics on separate lines |
| `S` | Display/toggle system processes |
| `^L` | Redraw screen |
| `h or ?` | Display summary of interactive keystrokes |
| `k` | Kill processes whose space-separated PID-list is specified |
| `n or #` | Change the number of processes to display |
| `o or O` | Other-filtering—You will be prompted for the selection criteria which then determines which tasks will be shown in the “current” window |
| `r` | Change the nice value of a list of processes specified as space-separated PIDs |
| `s` | Change periodic update time (in seconds) |
| `t` | Toggle the display of top process |
| `z` | Switches the “current” window between your last used color scheme and the older form of black-on-white. |

## TABLE 10.8

### Default Fields of the Output of the top Command with Brief Descriptions

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

```text
$ top
top - 21:17:44 up 82 days,  2:25,  3 users,  load average: 0.37, 0.28, 0.29
Tasks: 178 total,   1 running, 177 sleeping,   0 stopped,   0 zombie
%Cpu(s):  7.7 us,  0.2 sy,  0.0 ni, 92.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem :  8079236 total,  2255528 free,  231152 used,  5592556 buff/cache
KiB Swap:  8292348 total,  8206680 free,    8568 used.  7063932 avail Mem

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
24303 root      20   0  123204   7532   6392 S   0.7  0.1   0:00.06 sshd
24302 sarwar    20   0   42116   3780   3160 R   0.3  0.0   0:00.04 top
    1 root      20   0  119836   4664   2976 S   0.0  0.1   1:42.38 systemd
    2 root      20   0       0      0      0 S   0.0  0.0   0:00.81 kthreadd
    3 root      20   0       0      0      0 S   0.0  0.0   0:13.36 ksoftirqd/0
    5 root       0 -20       0      0      0 S   0.0  0.0   0:00.00 kworker/0:+
    7 root      20   0       0      0      0 S   0.0  0.0 113:00.38 rcu_sched
```

While running a command in the foreground, you might need to suspend it in order to go back to the shell, do something under the shell, and then return to the suspended process. For example, say that you are in the middle of editing a C program file with vim and need to compile the program to determine whether some errors have been corrected. You can save changes to the file, suspend vim, compile the program to view the results of the compilation, and return to vim. You can suspend a foreground process by pressing <Ctrl+Z>, move a suspended process to the foreground by using the fg command, and move a suspended process to the background by using the bg command. So you can suspend vim by pressing <Ctrl+Z>, compile the program to identify any other errors, and resume the suspended vim session by using the fg command.

```text
Syntax:
  fg [%jobid]
  bg [%jobid-list]
Purpose: Syntax 1: Resume execution of the process with job number jobid in the foreground or move background processes to the foreground; a jobid starts with %
Syntax 2: Resume execution of suspended processes/jobs with job numbers in jobid-list in the background; a jobid starts with %
Commonly used options/features:
  % or %+   Current job
  %-        Previous job
  %N        Job number N
  %name     Job beginning with name
  % ?name   Command containing name
```

If there are multiple suspended processes, the fg command without an argument brings the current process into the foreground, and the bg command without an argument resumes execution of the current process in the background. The job using the CPU at any particular time is called the current job.
You can use the jobs command to display the job numbers of all suspended (stopped) and background processes and identify which one is the current process. The current process is identified by a + and the previous process by a – in the output of the jobs command. The following is a brief description of the command.

```text
Syntax:
  jobs [option] [%jobid-list]
Purpose: Display the status of the suspended and background processes specified in jobid-list; with no list, display the status of current job
Commonly used option/feature:
  -l   Also display PIDs of jobs
```

In the following sessions, we show the use of the fg, bg, <Ctrl+Z>, and jobs commands. It is assumed here that the example file bigdata is very large and takes a long time to sort and copy! Otherwise, your commands and the processes they generate don’t live long enough to show up as running processes unless they comprise of infinite loops such as a C program like int main() { for(;); }.
We run the sort and cp commands in the background. The jobID and PID pairs of these processes are [1] 60149 and [2] 60156 for the sort and cp commands, respectively. The sort bigdata command is in the currently running process/job, as shown in the output of the jobs and jobs -l commands, as well as the R state of the process in the output of the ps command. The cp bigdata bigdata1 command has been swapped on the disk, as indicated by the D state of the process in the output of the ps command.

```text
$ sort bigdata > bigdata.sorted &
[1] 60149
$ cp bigdata bigdata1 &

```

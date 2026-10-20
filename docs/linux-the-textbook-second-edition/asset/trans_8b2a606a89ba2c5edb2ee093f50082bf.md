

## 表10.6

### Linux Mint 中 top 命令的头部信息

```text
top - 14:07:29 up 30 days, 21:30, 1 user, load average: 0.50, 0.36, 0.31
Tasks: 250 total, 1 running, 248 sleeping, 0 stopped, 1 zombie
%Cpu(s): 7.0 us, 3.9 sy, 0.0 ni, 88.9 id, 0.0 wa, 0.0 hi, 0.2 si, 0.0 st
KiB Mem : 5981672 total, 833348 free, 975496 used, 4172828 buff/cache
KiB Swap: 6157308 total, 6155404 free, 1904 used. 4641868 avail Mem
```

这取决于运行该命令的 Linux 发行版。头部信息可以包括负载平均值、系统已运行的时间（天+小时:分钟:秒）、当前时间、系统中的进程数、睡眠进程数、僵尸进程数、CPU 利用率（空闲时间、用户时间、内核/系统时间以及中断处理时间的百分比）、主内存中用户区的利用率（总量和空闲量）以及交换空间（总量和空闲量）。表10.6列出了 Linux Mint 中 top 命令的头部信息。

top 命令的大部分功能可以在 top 运行时通过交互式按键命令来选择。下面的语法框给出了常用的命令行选项，表10.7简要描述了 top 命令的交互式按键。

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

在下面的文本中，我们展示了 top 命令输出的示例会话。下面是不带任何选项运行该命令的情况。命令输出显示系统已连续运行 82 天没有崩溃。此外，系统中当前有 178 个进程，其中 1 个在运行，177 个在睡眠，0 个停止或处于僵尸状态。属于 root 的 systemd 进程是 PID 1。rcu_sched 进程（PID 7）及其已终止的子进程已使用了 112 小时 59.23 秒的 CPU 时间。你可以通过表10.8了解头部和其他进程属性中的值的含义。如果观察命令输出一段时间，你会发现进程会随着其优先级的变化而上下移动。同样，头部中的统计信息也会定期更新。还要注意，PID 1 被列为 systemd，即该进程的程序名称，而不是命令的路径。我们可以在 Linux Mint 系统上使用 c 交互式 top 命令来切换 COMMAND 列的显示，以显示执行这些进程的命令路径。

## 表10.7

### top 的部分交互式按键命令简述

| Command | Meaning |
|---|---|
| `H` | 在单独的行上显示/切换线程统计信息 |
| `S` | 显示/切换系统进程 |
| `^L` | 重绘屏幕 |
| `h or ?` | 显示交互式按键的摘要 |
| `k` | 终止指定的以空格分隔的 PID 列表所对应的进程 |
| `n or #` | 更改要显示的进程数量 |
| `o or O` | 其他过滤——系统会提示你输入选择条件，该条件将决定哪些任务会显示在“当前”窗口中 |
| `r` | 更改以空格分隔的 PID 列表所指定的进程的 nice 值 |
| `s` | 更改定期更新时间（秒） |
| `t` | 切换 top 进程的显示 |
| `z` | 在最近使用的配色方案和旧版白底黑字之间切换“当前”窗口。 |

## 表10.8

### top 命令输出的默认字段及其简要说明

| Field | Description |
|---|---|
| `%CPU` | CPU 使用率——自上次屏幕更新以来任务所消耗的 CPU 时间占比，以总 CPU 时间的百分比表示 |
| `%MEM` | 内存使用率（RES）——任务当前占用的可用物理内存的比例 |
| `COMMAND` | 命令名或命令行——显示用于启动任务的命令行或关联程序的名称 |
| `NI` | nice 值——任务的 nice 值。负的 nice 值表示较高的优先级，而正的 nice 值表示较低的优先级 |
| `PID` | 进程 ID——任务唯一的 PID，会周期性回绕，但绝不会在零处重新开始 |
| `PR` | 优先级——任务的调度优先级 |
| `RES` | 常驻内存大小（KiB）——任务正在使用的非交换物理内存 |
| `S` | 进程状态——任务的状态，可以是以下之一：D = 不可中断的睡眠，R = 运行，S = 睡眠，T = 被作业控制信号停止，t = 在跟踪期间被调试器停止，Z = 僵尸 |
| `SHR` | 可共享的 VIRT 内存量 |
| `TIME+` | CPU 时间，百分之一秒——与 TIME 相同，但通过百分之一秒的粒度更精细 |
| `USER` | 用户名——任务所有者的有效用户名 |
| `VIRT` | 虚拟内存大小（KiB）——任务使用的虚拟内存总量。它包括所有代码、数据和共享库，以及已换出的页面和已映射但未使用的页面 |

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

在前台运行命令时，你可能需要挂起它以便返回 shell，在 shell 下执行一些操作，然后再回到被挂起的进程。例如，假设你正在用 vim 编辑一个 C 程序文件，并且需要编译该程序以确认一些错误是否已修正。你可以保存对文件的修改，挂起 vim，编译程序以查看编译结果，然后返回 vim。你可以通过按 <Ctrl+Z> 挂起前台进程，使用 fg 命令将被挂起的进程移到前台，使用 bg 命令将被挂起的进程移到后台。因此，你可以通过按 <Ctrl+Z> 挂起 vim，编译程序以找出其他错误，然后使用 fg 命令恢复被挂起的 vim 会话。

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

如果有多个挂起的进程，不带参数的 fg 命令会将当前进程带入前台，而不带参数的 bg 命令会在后台恢复当前进程的执行。在任意特定时刻使用 CPU 的作业称为当前作业。你可以使用 jobs 命令显示所有挂起（停止）和后台进程的作业号，并识别哪个是当前进程。在 jobs 命令的输出中，当前进程用 + 标识，上一个进程用 – 标识。下面是对该命令的简要说明。

```text
Syntax:
  jobs [option] [%jobid-list]
Purpose: Display the status of the suspended and background processes specified in jobid-list; with no list, display the status of current job
Commonly used option/feature:
  -l   Also display PIDs of jobs
```

在下面的会话中，我们展示了 fg、bg、<Ctrl+Z> 和 jobs 命令的使用。这里假设示例文件 bigdata 非常大，排序和复制需要很长时间！否则，你的命令及其产生的进程存活时间太短，无法显示为运行中的进程，除非它们包含无限循环，比如像 int main() { for(;); } 这样的 C 程序。我们在后台运行 sort 和 cp 命令。这些进程的作业号和 PID 对分别是 sort 和 cp 命令的 [1] 60149 和 [2] 60156。正如 jobs 和 jobs -l 命令的输出以及 ps 命令输出中进程的 R 状态所示，sort bigdata 命令是当前正在运行的进程/作业。cp bigdata bigdata1 命令已被交换到磁盘上，这由 ps 命令输出中进程的 D 状态所指示。

```text
$ sort bigdata > bigdata.sorted &
[1] 60149
$ cp bigdata bigdata1 &

```


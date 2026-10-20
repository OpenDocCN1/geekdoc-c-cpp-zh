

# 表 10.5

## 计算 Linux 进程优先级的重要参数

| 参数 | 值 |
|---|---|
| MAX_NICE | 19 (对进程最不利) |
| MIN_NICE | -20 (对进程最有利) |
| NICE_WIDTH | (MAX_NICE - MIN_NICE + 1) = 40 |
| MAX_RT_PRIO | 100 |
| MAX_PRIO | (MAX_RT_PRIO + NICE_WIDTH) = 100 + 40 = 140 |
| DEFAULT_PRIO | (MAX_RT_PRIO + NICE_WIDTH / 2) = (100 + 40/2) = 120 |

进程的优先级可以为 0–139。RT 进程的优先级可以为 0–99。用户进程，即 SCHED_NORMAL/SCHED_OTHER（普通）和 SCHED_BATCH（批处理）进程的优先级为 100–139。为方便起见，在处理各种调度器参数时，该优先级范围被转换为 0–39，只需从给定的优先级值中减去 MAX_RT_PRIO 即可。这是可以分配给 nice 值并受 nice 和 renice 命令影响的优先级范围。你可以使用通用命令 nice -n nice_value program_name 以所需的优先级启动程序。同样，你也可以使用通用命令 renice -n nice_value -p process_id 更改已运行进程的优先级。

以下是我们在 Linux Mint 系统上 ps 命令的输出，系统运行在 multi-user.target 级别，并请求输出调度优先级类（CLS）、调度优先级（PRI）和 nice 值（NI）的格式，以及一些标准标识输出格式列。

```
$ ps -ax --format uname,pid,ppid,tty,cmd,cls,pri,nice
USER       PID  PPID TT       CMD                     CLS PRI NI
root         1     0 ?       /sbin/init splash        TS  19  0
root         2     0 ?       [kthreadd]               TS  19  0
root         3     2 ?       [ksoftirqd/0]            TS  19  0
root         5     2 ?       [kworker/0:0H]           TS  39 -20
root         7     2 ?       [rcu_sched]              TS  19  0
root         8     2 ?       [rcu_bh]                 TS  19  0
root         9     2 ?       [migration/0]            FF 139  -
root        10     2 ?       [watchdog/0]             FF 139  -
...
[output truncated]
...
root     21936     2 ?       [kworker/u16:1]          TS  19  0
root     21942  1128 ?       sshd: sarwar [priv]      TS  19  0
sarwar   21944     1 ?       /lib/systemd/systemd --user TS 19 0
sarwar   21946 21944 ?       (sd-pam)                 TS  19  0
sarwar   21960 21942 ?       sshd: sarwar@pts/0       TS  19  0
sarwar   21961 21960 pts/0   -bash                    TS  19  0
sarwar   21982 21961 pts/0   ps -ax --format uname,pid,p TS 19 0
root     22407     1 tty1    /bin/login --            TS  19  0
root     22876     2 ?       [kworker/6:0]            TS  19  0
$
```

/sbin/init splash 命令被运行以创建 systemd，其优先级为 19 且类为 TS（SCHED_OTHER）。Systemd 是一个系统管理守护进程、实用程序和库的集合，作为经典 init 守护进程的替代品，最初为 System V UNIX 设计。它是所有用户级进程和守护进程的父进程。内核线程守护进程 kthreadd 也是如此。请注意，所有属于 sarwar 的进程的优先级值都与 systemd 相同，类和优先级也相同。有关 systemd 的更多信息、其服务启动功能以及它如何在单元文件中分配资源，请参阅第 20 章。

chrt 命令设置或检索正在运行进程的 RT 调度属性，或以指定属性运行命令。你可以设置或检索进程的调度策略和优先级。Linux 使用的默认调度策略是 SCHED_OTHER（或 SCHED_NORMAL）。不带任何参数运行时，chrt 显示其使用方法的简要摘要，如以下会话所示。

```
$ chrt
Show or change the real-time scheduling attributes of a process.

Set policy:
  chrt [options] <priority> <command> [<arg>...]
  chrt [options] -p <priority> <pid>

Get policy:
  chrt [options] -p <pid>

Policy options:
  -b, --batch          set policy to SCHED_BATCH
  -f, --fifo           set policy to SCHED_FIFO
  -i, --idle           set policy to SCHED_IDLE
  -o, --other          set policy to SCHED_OTHER
  -r, --rr             set policy to SCHED_RR (default)

Scheduling flag:
  -R, --reset-on-fork  set SCHED_RESET_ON_FORK for FIFO or RR

Other options:
  -a, --all-tasks      operate on all the tasks (threads) for a given pid
  -m, --max            show min and max valid priorities
  -p, --pid            operate on existing given pid
  -v, --verbose        display status information

  -h, --help           display this help and exit
  -V, --version        output version information and exit

For more details see chrt(1).
$
```

chrt -m 命令的输出显示 SCHED_OTHER/SCHED_NORMAL、SCHED_BATCH、SCHED_IDLE 策略仅允许优先级 0，而 SCHED_FIFO 和 SCHED_RR 的范围为 1 到 99。

```
$ chrt -m
SCHED_OTHER min/max priority  : 0/0
SCHED_FIFO min/max priority   : 1/99
SCHED_RR min/max priority     : 1/99
SCHED_BATCH min/max priority  : 0/0
SCHED_IDLE min/max priority   : 0/0
$
```

在以下会话中，我们使用 ps 命令显示当前进程的状态，包括 PID 为 27223 的 bash。chrt -p 27223 命令显示 bash 的 RT 调度属性。属性为当前调度策略和进程的当前优先级。

```
$ ps
    PID TTY          TIME CMD
  27223 pts/0    00:00:00 bash
  27330 pts/0    00:00:00 ps
```

```
$ chrt -p 27223
pid 27223's current scheduling policy: SCHED_OTHER
pid 27223's current scheduling priority: 0
$
```

以下会话中的第一个命令用于将 bash 的调度策略从 SCHED_OTHER 更改为 SCHED_BATCH。第二个命令显示新的调度策略为 SCHED_BATCH，调度优先级为 0。

```
$ chrt -b -p 0 27223
$ chrt -p 27223
pid 27223's current scheduling policy: SCHED_BATCH
pid 27223's current scheduling priority: 0
$
```

你 Linux 系统上的 sched 手册页描述了 CPU 调度的 API。

在以下章节练习中，你将使用带或不带选项的 ps 命令来了解命令输出。

## 练习 10.7

使用 ps 命令显示当前会话中正在运行的进程的状态。你能识别出你的登录 shell 吗？它是什么？

## 练习 10.8

运行命令以显示系统上运行的所有进程的状态。你运行了什么命令？它们的 PID 是什么？所有进程的父进程的 PID 是什么？

## 练习 10.9

在你的 Linux 系统上复制之前涉及 chrt 命令的会话，以验证其按预期工作。

### 10.5.3 进程属性的动态显示

有时，你想识别失控进程或特定用户的进程未推进（即卡住的进程）。Linux top 命令允许你通过实时报告进程的 CPU 活动和属性来执行这些任务。它按默认情况下按以下从左到右显示的进程属性显示系统上最耗 CPU 的进程：

PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND

其中 PID 是进程 ID 号，USER 是所有者的有效用户名，PR 是进程优先级，NI 是进程 nice 值，VIRT 是进程在虚拟内存中的大小，SHR 是进程可用的共享内存量，RES 是进程的驻留部分（即进程在主内存中的当前大小），S 是进程状态，%CPU 是进程使用的 CPU 时间百分比，%MEM 是进程使用的内存量，TIME+ 是进程已执行的时间量，COMMAND 是用于调用进程的命令名。要查看可显示的进程属性的更完整的字母顺序列表，请参阅系统上 top 的手册页。

top 命令会一直运行，直到你按下 <q> 或 <Q>，并每秒左右更新一次状态。周期性更新时间可以在执行 top 命令时通过命令行选项指定，也可以在 top 运行期间通过交互式命令指定。要显示的状态进程数取决于显示屏的大小或基于图形用户界面（GUI）的系统上的窗口大小。在智能显示器或窗口上，通常为 15–30 行，每行一个进程。

该命令还在一个简短的头部中显示其他重要的系统统计信息，包含五到八行，在进程和/或线程的统计信息之前显示。头部信息


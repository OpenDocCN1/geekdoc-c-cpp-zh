
# 计算系统的性能、可靠性和可用性评估

……若干选项。要深入了解其选项和格式，请参考 `man lsof`。当未指定选项时，lsof 会打开所有活动进程的文件。例如，考虑命令行 `lsof -p 29003`，其中 29003 是名为 `cwf` 的进程的 pid。执行该命令时，显示了如下数据：

| COMMAND | PID USER | FD | TYPE | SIZE/OFF | NODE NAME |
|---|---|---|---|---|---|---|
| cwf | 29003 cwf | DIR | DIR | 8 | 4096 | 942333 /home/prm/Measuring/C |
| cwf | 29003 | rtd | | 8 | 4096 | 2 |
| cwf | 29003 | txt | REG | 8 | 7596 | 942328 /home/prm/Measuring/C |
| cwf | 29003 | mem | REG | 8 | 1768484 | 130587 |
| cwf | 29003 | | | | 8 | | /lib/x86_64-linux-gnu/libc-2.23.so |
| cwf | 29003 | mem | REG | 8 | 147688 | 130563 /lib/ih-linux-gnu/ld-2.23.so |
| cwf | 29003 | | | CHR | 136 | 2 | 5 /dev/pts2 |
| cwf | 29003 | 2u | CHR | 136 | 2 | 5 /dev/pts2 |
| cwf | 29003 | 3w | REG | 8 | 0 | 943269 /home/prm/Measuring/C/file.txt |

内容显示了两个目录 `/home/prm/Measuring/C` 和 `/proc`，两个库文件（libc-2.23.so 和 ld-2.23.so），三个字符设备文件 (`/dev/pts2`)，一个包含 pid = 29003 (cwf) 进程代码的文件，以及一个数据文件 (file.txt)。

# 命令 /usr/bin/time

`/usr/bin/time` 命令用于计算执行给定命令所需的时间。它对于测量脚本和命令的执行时间有用。分析人员应该注意，大多数 Linux shell 都有内置的 `time` 命令版本。例如，如果在 bash shell 中执行命令 `time`，显示输出为 `time`。另一方面，如果运行命令行 `/usr/bin/time`，显示输出同样为 `time`。同理，在 shell 中执行 `time`，显示输出也是 `time`。因此，如果需要使用 GNU `time` 命令，分析人员必须指定 time 二进制文件的完整路径，通常为 `/usr/bin/time`。输出格式可以通过 `-f` 字符串进行配置，其中命令是要测量的执行时间的实用程序。该字符串是一个 ASCII 字符串，用符号 `%` 前的字母表示指定的关键字。因此，当执行命令行 `time -f "Elapsed Time (s) %E"` 时，显示输出类似于 `Elapsed Time (s) 0.05`。执行命令 `/usr/bin/time` 时显示的信息由以下关键字定义：

- c 指定由于时间分片导致的上下文切换次数。
- C 指定被测量命令的名称和参数。
- D 显示共享数据的平均大小 (KB)。
- e 显示经过的时间。
- E 显示经过的时长（时:分:秒）。
- F 描述输入/输出故障的次数。
- I 描述文件系统的输入次数。
- k 描述传递给进程的信号数。
- K 显示平均总数据 (KB)。
- M 描述最大驻留内存 (KB)。
- O 描述文件系统的输出次数。
- p 显示平均未共享大小 (KB)。
- P 显示处理器利用率。
- r 描述接收到的消息数。
- R 显示可恢复错误的数量。
- s 显示发送的消息数。
- S 显示系统使用的总处理器时间（秒）。
- t 提供平均驻留大小 (KB)。
- U 提供由进程直接使用的处理器时间（秒）。
- w 提供自愿切换的次数。
- W 描述进程被换出主内存的次数。
- x 描述退出状态。
- X 提供平均共享大小 (KB)。
- Z 系统页面大小（字节）。

另一个例子，考虑执行命令行 `/usr/bin/time -f "Elapsed Time (s) %E, Maximum Resident Size (KB) %M"` /home/prm/Measuring/C。该命令显示了执行时间，以及该进程代码在其生命周期内的最大驻留内存。输出：`Elapsed Time (s) 7.77, Maximum Resident Size (KB) 980`。

# 性能测量

# 命令 date

`date` 命令是 Linux 系统中广泛使用的工具。该命令用于显示或设置系统的日期和时间。有许多选项可以自定义输出，例如设置日期和时间、以各种格式呈现信息、计算日期，甚至设置系统时钟。该命令的标准语法为 "date options"。`date` 命令支持许多选项和输出格式。要详细查看可用选项，请参考 "man date"。在这里，我们介绍了一些支持测量事件之间持续时间的有用选项。因此，我们没有先介绍其选项再描述一些有用示例，而是针对这些示例讨论相应的选项和格式。不带任何参数的 `date` 命令显示当前日期和时间，例如：

```
Fri May 29 14:34:11 -03 2020
```
24 小时格式 (hh:mm:ss)，时区为 GMT。例如，哪条命令以 ISO 8601 格式显示日期和时间，其中“小时”、“分钟”、“秒”或“ns”（纳秒）定义了精度。

```
date --iso-8601-hours (command line)
2020-05-29T16:03:00 (output),
```

```
date --iso-8601-minutes (command line)
2020-05-29T16:03 (output),
```

```
date --iso-8601-seconds (command line)
2020-05-29T16:03:00 (output),
```

```
date --iso-8601-ns (command line)
2020-05-29T16:03:00.000000000 (output),
```

执行该命令显示的信息的是符合 RFC 3339 格式的日期和时间，其中“ns”定义了精度。

- 小时 - 分钟 - 秒。
- 格林治时间。
- https://www.iso.org/iso-8601-date-and-time.html。
- https://tools.ietf.org/html/rfc3339。

```
date --rfc-3339-ns (command line)
2020-05-29T16:53:59.899910494-03:00 (output),
```
接下来的命令以 24 小时格式 (hh:mm:ss) 显示当天时间。

```
date +T (command line)
16:55:26 (output),
```
执行下面的命令显示当前时间的位置表示。

```
date +X (command line)
04:56:17 PM (output),
```
`date` 工具还包含一个有趣的特性，它可以将当前时间表示为从 Unix Epoch到当前时间的秒数。这对于计算事件之间的持续时间非常有吸引力。以下命令提供了此类信息：

```
date +%s (command line)
1590782231 (output),
```
接下来的命令描述秒的小数。

```
date +%s.%N (command line)
1590782234.256798180 (output),
```
结束和开始之间的差值为 1.040994s。

# 计算系统的性能、可靠性和可用性

# 性能测量

# 脚本

```bash
#!/bin/bash
#Filename: time_take.sh
start=$(date +%s%N)
~/home/prm/Measuring/C
~/home/prm/Measuring/C
end=$(date +%s%N)
echo "Epoch Before $start."
echo "Epoch After $end"
```
Time Epoch Before 1590788876.851077030 秒。
Time Epoch After 1590788877.855176470 秒。


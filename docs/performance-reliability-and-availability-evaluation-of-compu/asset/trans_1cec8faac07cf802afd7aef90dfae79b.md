

## 438 计算系统的性能、可靠性和可用性评估

### 算法 14 CPU 利用率 - 采集脚本 - 练习 28

```
printf "CPU Utilization \n" >> cpu_util.txt;
for i in (1..100)
do
  top -b -n 1 | awk 'NR=3{printf "%.3f%% \n", ($2+$4+$6+$12+$14+$16)/100}'
  sleep 60;
done
```

- (b) 分析采集到的样本，提供其统计摘要和合适的图表来表示该样本。
- (c) 编写总结，解释样本以及系统可能的特征。
- (d) 使用 dstat 采集样本以代替上述脚本。
- (e) 对采用 dstat 的优缺点进行评论。

**练习 29.** 脚本 15 通过 `top` 命令收集了一个大小为 100 的 CPU 利用率样本。测量之间的延迟为 120 秒。在每次采集时，捕获每个状态下的 CPU 利用率：us, sy, ni, id, wa, hi, 和 st。脚本产生一个列格式的 txt 文件。

### 算法 15 使用 `iostat` 命令考虑状态类别的 CPU 利用率 - 练习 29

```
iostat | awk 'NR=3{printf "%s \t%s \t%s \t%s \t%s \t%s \t%s\n", $2,$3,$4,$5,$6,$7}'
  >> iostat_cpu_utilization.txt;
for i in (1..50)
do
  iostat | awk 'NR=4{printf "%.2f\t%.2f\t%.2f\t%.2f\t%.2f\t%.2f\t%.2f\n", $2,$3,$4,$5,$6,$7}'
  >> iostat_cpu_utilization.txt;
  sleep 60;
done
```

- (a) 对计算机模型、计算机系统当前状态、处理器数量、操作系统、正在执行的应用程序以及性能策略进行简短描述，并执行脚本 15。
- (b) 分析样本并提供统计摘要和图表来表示采集的数据。

## 性能测量 439

- (c) 编写总结，描述并解释样本以及系统可能的特征。
- (d) 使用 dstat 采集样本以代替上述脚本。
- (e) 对采用 dstat 的优缺点进行评论。

**练习 30.** 调整脚本 16（提示：调整脚本第 4 行的 NR），并收集一个覆盖系统每个设备的大小为 100 的 IO 流量样本。测量之间的延迟为 60 秒（参见 `iostat` 命令描述）。样本存储在 txt 文件中。

### 算法 16 使用 `iostat` 进行 IO 监控 - 练习 30

```
iostat | awk 'NR=6{printf "%s %s %s %.2f %.2f %.2f %s %d %d\n", $1, $2, $3, $4, $5, $6} >> iostat_io_tps.txt;
for i in {1..10}
  iostat | awk 'NR=8{printf "%s %.2f %.2f %.2f %s %d %d\n", $1, $2, $3, $4, $5, $6} >> iostat_io_tps.txt';
sleep 5;
done
```

- (a) 编写系统描述，例如计算机模型、计算机系统当前状态、处理器数量、操作系统、正在执行的应用程序以及性能策略。
- (b) 执行脚本 16，分析样本，提供其统计摘要和图表。
- (c) 采用适当的方法（见第 6 章）并获取每个指标的相应置信区间，假设置信度为 95%。
- (d) 编写总结，解释采集到的数据以及采集这些数据的系统。
- (e) 使用 dstat 采集样本以代替上述脚本。
- (f) 对采用 dstat 的优缺点进行评论。

**练习 31.** 编写脚本通过 `iostat` 命令收集一个大小为 100 的 CPU 利用率样本。测量之间的延迟为 240 秒。在每次采集时，捕获每个特定状态下的 CPU 利用率：user, nice, system, iowait, steal, 和 idle。脚本应产生一个按列整理的 txt 文件。

## 440 计算系统的性能、可靠性和可用性评估

- (a) 编写系统的简短描述，提到计算机模型、处理器数量、操作系统和正在执行的应用程序。
- (b) 执行脚本，分析样本并提供其统计摘要。
- (c) 编写总结解释采集到的数据。
- (d) 使用 dstat 采集样本以代替上述脚本。
- (e) 对采用 dstat 的优缺点进行评论。

**练习 32.** 执行脚本 17，并收集一个 50 次的域名 ping 延迟样本（例如：www.google.com 或其他）。测量之间的延迟为 10 秒。样本存储在 txt 文件中。

### 算法 17 从域名收集 Pinging 的样本 - 练习 32

```
printf "Ping Delay \n" >> pingtim.txt;
for i in (1..50)
do
    ping -c 1 www.google.com | awk -F"time=" NR=2{gsub(/ms/,"",$2);
        print $2 } >> pingtim.txt
    sleep 10
done
```

- (b) 分析样本，提供其统计摘要并对结果进行评论。

**练习 33.** 脚本 18 (tcpdumpscript.sh) 收集计算机所有接口上一个小时的网络流量。将网络流量存储在原始数据文件中 (any.pcap)。之后，它会杀死执行 `tcpdump` 命令的进程，从原始数据文件生成压缩文件 (any.pcap.tar.gz)，并删除原始数据文件 (any.pcap)。该脚本文件使用 root 用户安装在 /usr/bin 目录下。该脚本被计划在凌晨 02:00 开始运行。通过 cron 执行。

## 441 性能测量

值得注意的是，第一个字段 (02)、第二个字段、第三个、第四个和第五个字段分别代表日、月、日。符号 (*) 表示任意。crontab 显示如下：
02 * * * * /usr/bin/tcpdumpscript.sh

脚本 18 (tcpdumpscript.sh) 收集计算机所有接口上一个小时的网络流量。将网络流量存储在原始数据文件中 (any.pcap)。之后，它会杀死执行 `tcpdump` 命令的进程，从原始数据文件生成压缩文件 (any.pcap.tar.gz)，并删除原始数据文件 (any.pcap)。该脚本文件使用 root 用户安装在 /usr/bin 目录下。该脚本被计划在凌晨 02:00 开始运行。通过 cron 执行。

```bash
#!/bin/bash
tcpdump -i any -w any.pcap &
PID=$!
sleep 3600
kill $PID
tar -czf any.pcap.tar.gz any.pcap
rm any.pcap
```

第一个字段 (02)、第二个字段、第三个、第四个和第五个字段分别代表日、月、日。符号 (*) 表示任意。crontab 显示如下：
02 * * * * /usr/bin/tcpdumpscript.sh

脚本 18 (tcpdumpscript.sh) 收集计算机所有接口上一个小时的网络流量。将网络流量存储在原始数据文件中 (any.pcap)。之后，它会杀死执行 `tcpdump` 命令的进程，从原始数据文件生成压缩文件 (any.pcap.tar.gz)，并删除原始数据文件 (any.pcap)。

算法 18 网络监控 使用 tcpdump -


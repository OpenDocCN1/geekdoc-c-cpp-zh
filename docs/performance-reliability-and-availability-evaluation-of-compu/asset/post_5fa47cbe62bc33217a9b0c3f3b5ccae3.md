
# Performance, Reliability, and Availability Evaluation of Computational Systems

several options. For an in-depth view of its options and formats, refer to man lsof. When no option is specified, lsof opens the files of all active processes. For an example, consider the command line `lsof -p 29003`, where 29003 is the pid of a process named cwf. When the command was executed, the data was displayed.

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

In the contents show two directories /home/prm/Measuring/C and /proc, two libraries (libc-2.23.so and ld-2.23.so), three character-device files (/dev/pts2), one file that contains the code of the process whose pid = 29003 (cwf), and one data file (file.txt).

# Command /usr/bin/time

The /usr/bin/time command is used to calculate how long a given command takes to execute. It is useful to measure the execution time of scripts and commands. The analyst should be aware that most Linux shells have their built-in versions of the time command. For example, if the command `time` is executed in bash shell, the display output is `time`. On the other hand, if the command line `/usr/bin/time` is run, the display output is `time`. Likewise, executing `time` in shell, the display output is `time`. Therefore, if one needs to use the GNU time command, the analyst must specify the full path to the time binary, which is usually `/usr/bin/time`. The output format can be configured with the `-f` string, where command is the utility whose execution time is to be measured. The string is an ASCII string with specified keywords depicted by a letter preceded by the symbol %. Therefore, when the command line `time -f "Elapsed Time (s) %E"` is executed, the display output is similar to Elapsed Time (s) 0.05. The information shown by the execution of the command `/usr/bin/time` is defined by the following keywords:

- c specifies the number of context switches due to slicing.
- C specifies the name and arguments of the command being measured.
- D shows the average size of shared data (KB).
- e shows the elapsed time.
- E shows the elapsed hours:minutes:seconds.
- F depicts the number of input-output faults.
- I depicts the number of filesystem inputs.
- k depicts the number of signals delivered to the process.
- K shows the average total data (KB).
- M depicts the maximum resident size (KB).
- O depicts the number of filesystem outputs.
- p shows the average unshared size (KB).
- P shows the processor utilization.
- r depicts the number of messages received.
- R shows the number of recoverable faults.
- s shows the number of messages sent.
- S shows the total processor time (in seconds) used by the system.
- t presents the average resident size (KB).
- U presents the processor time (in seconds) directly by the process.
- w presents the number of voluntary switches.
- W depicts the number of times the process was swapped out of the main memory.
- x depicts the exit status.
- X presents the average shared size (KB).
- Z system page size (bytes).

Another example, consider the execution of the command line `/usr/bin/time -f "Elapsed Time (s) %E, Maximum Resident Size (KB) %M"` /home/prm/Measuring/C. This command displays the execution time, and the maximum resident size of the process whose code is its lifetime. Elapsed Time (s) 7.77, Maximum Resident Size (KB) 980.

# Performance Measuring

# Command date

The command date is a widely used tool in Linux-based systems. This command displays or sets the date and time of the system. There are many options for customizing its output, such as setting dates and times, presenting the information in various formats, calculating dates, and even setting the system clock. The standard syntax of the command is "date options". The date command supports many options and output formats. For a detailed view of the available options, please refer to "man date". Here, we present some useful options that supports measuring duration between events. Hence, instead of introducing its options and then depicting some useful examples, and for them, we discuss the respective options and formats. The command date without any arguments displays the current date and time, such as

```
Fri May 29 14:34:11 -03 2020
```
24-hour format (hh:mm:ss), and the time zone is GMT. For the example, which command display date and time in ISO 8601 format, where "hours", "minutes", "seconds", or "ns" (nanoseconds) defines the precision.

```
date --iso-8601-hours (command line)
2020-05-29T16:03:00 (output),
```

```
date --iso-8601-minutes (command line)
2020-05-29T16:52:03 (output),
```

```
date --iso-8601-seconds (command line)
2020-05-29T16:51:05-03 (output),
```

```
date --iso-8601=ns (command line)
2020-05-29T16:08:650258894-03 (output).
```

The next command displays date and time in RFC 3339 format, where "ns" defines the precision.

- hour - mm - minutes, and seconds.
- Greenwich Mean Time.
- https://www.iso.org/iso-8601-date-and-time-format.html.
- https://tools.ietf.org/html/rfc3339.

```
date --rfc-3339-ns (command line)
2020-05-29 16:53:59.899910494-03:00 (output).
```
The execution of the next command line displays the time of the day in 24-hour format (hh:mm:ss).

```
date +T (command line)
16:55:26 (output).
```
The execution of the command line below shows the time representation of the current place.

```
date +X (command line)
04:56:17 PM (output).
```
The command tool also includes this interesting feature where it can represent the current time as a count of the seconds from the UNIX epoch time to the current time. This is an attractive characteristic for calculating duration between events. The following command provides such information.

```
date +%s (command line)
1590782231 (output).
```
The next command depicts the fraction of nanoseconds.

```
date +%s.%N (command line)
1590782234.256798180 (output).
```
The difference between end and start was 1.040994s.

# Performance, Reliability, and Availability of Computational Systems

# Performance Measuring

# Performance, Reliability, and Availability Evaluation of Computational Systems

```bash
#!/bin/bash
#Filename: time_take.sh
start=$(date +%s%N)
~/home/prm/Measuring/C
~/home/prm/Measuring/C
end=$(date +%s%N)
echo Epoch Before $start.
echo Epoch After $end
```
Time Epoch Before 1590788876.851077030 seconds.
Time Epoch After 1590788877.855176470 seconds.

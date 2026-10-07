# Performance Measuring

The following example displays performance statistics specified by the process identified by pid (process identification), -p 5217. The time between samples is detected by the delay field value, in this case, 2s.

> pidstat -p 5217 2

A typical portion of data obtained by the command above is shown below.

```
11:06:06 AM UID PID %usr %system %guest %CPU CPU Command
11:06:08 AM 1000 5217 1.05 0.00 0.00 1.05 0 firefox
11:06:10 AM 1000 5217 1.04 0.52 0.00 1.56 0 firefox
11:06:12 AM 1000 5217 1.05 0.00 0.00 1.05 0 firefox
11:06:14 AM 1000 5217 0.53 0.00 0.00 1.58 0 firefox
```

We use pidstat to obtain input-output statistics about a process by adopting the option -d. As an example, the following command line asks samples of input-output statistics of the process specified by -p 19635, where the time between samples is 2s.

> pidstat -p 19635 -d 2

A typical chunk of data obtained by the command is depicted below.

```
06:14:32 PM UID PID KB/rd/s KB/wr/s kB-ccw/s idle CPU Command
06:14:37 PM 1000 19635 71.52 0.00 0.00 3 firefox
06:14:42 PM 1000 19635 147.57 2475.08 0.00 10 firefox
06:14:47 PM 1000 19635 266.67 141.41 1.35 0 firefox
06:14:52 PM 1000 19635 25.60 43.86 0.00 1 firefox
06:14:57 PM 1000 19635 93.39 49.56 1.84 2 firefox
06:15:02 PM 1000 19635 0.00 22.59 0.00 0 firefox
06:15:07 PM 1000 19635 1484.62 173.85 0.00 10 firefox
06:15:12 PM 1000 19635 0.00 3.77 0.00 0 firefox
06:15:17 PM 1000 19635 0.00 4.23 0.00 0 firefox
```

]
nThe command pidstat may be used to find a memory leak using the following command.

> pidstat -p 5217 -r 5

This command-line reports samples of page faults statistics of the process specified by -p 5217. The time between samples is 5s. A command supports supporting memory leaking problems.

```
11:11:42 AM 1000 5217 0.00 0.00 1209512 368116 17.86 firefox
11:11:47 AM 1000 5217 0.00 0.00 1209512 368116 17.86 firefox
11:11:52 AM 1000 5217 0.21 0.00 1209512 368116 17.86 firefox
11:11:57 AM 1000 5217 162.41 1.13 121121 367872 17.84 firefox
11:12:02 AM 1000 5217 221.09 13.28 1219176 368016 17.85 firefox
11:12:07 AM 1000 5217 1373.02 31.75 1221104 372248 18.06 firefox
```
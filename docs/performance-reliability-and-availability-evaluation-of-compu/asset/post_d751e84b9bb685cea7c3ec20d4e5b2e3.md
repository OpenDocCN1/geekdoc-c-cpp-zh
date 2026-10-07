
## Performance Measuring

The various entries in the /proc virtual file system are described extensively in the /proc man page five, which is obtained by executing “man 5 proc”. Below, we provide some useful entries of the content available in the /proc virtual filesystem and briefly introduces some basic Linux monitoring tools.

## 23.7.1 SYSTEM INFORMATION

This section presents some important basic Linux monitoring tools. The monitoring tools usually get information from entries available in the virtual filesystem /proc. This virtual filesystem may be regarded as an information and control center for the Linux kernel, and any monitoring and configuring utilities calls files in /proc. Some useful entries contained in /proc are depicted below, and some of them are detailed further.

- /proc/sys/kernel/hostname holds the domain name.
- /proc/sys/kernel/hostname contains the computer's host name.
- /proc/cpuinfo carries data specifying processors and system architecture.
- /proc/meminfo holds statistics on memory usage.
- /proc/ostype contains the OS type.
- /proc/version carries the Linux kernel version number.
- /proc/osrelease holds the kernel Linux version revision.
- /proc/stat contains processors and memory usage information.
- /proc/loadavg holds information about the system load.
- /proc/uptime carries the idle duration since the boot.
- /proc/devices contains the character and block devices currently configured.
- /proc/diskstat holds the I/O statistics of block devices.
- /proc/iomem holds the current map of the system's memory for each physical device.
- /proc/ports contains a list of currently registered ports used for input or output communication with a device.

Executing the command “cat /proc/entry” provides the respective content of the entry. Below, we display the content of /proc/cpuinfo and /proc/meminfo entries as examples.

## Entry /proc/cpuinfo

The entry /proc/cpuinfo provides a collection of data specifying the processors and system architecture dependent. Two common entries are processor, gives the processor number, and BogoMips^9, a system constant that is calculated during kernel initialization. We have a chunk of data provided through this entry.

```
processor : 0
vendor_id : GenuineIntel
cpu family : 6
model : 142
model name : Intel(R) Core(TM) i5-7200U CPU @ 2.50GHz
stepping : 9
microcode : 0xe8
cpu MHz : 2712.004
ache size : 3072 KB
...
bogimips : 5424.00
clflush size : 64
cache_alignment : 64
address size : 43 bits physical, 48 bits virtual
```

## Entry /proc/meminfo

The entry /proc/meminfo file reports statistics about the system's memory usage. The content provided, though, may slightly differ between Linux systems. Below we have a portion of the data content commonly provided through this entry.

```
MemTotal: 2061512 kB
MemFree: 283080 kB
MemAvailable: 619608 kB
Buffers: 35512 kB
Cached: 506112 kB
SwapCached: 4512 kB
...
```

## Command uname

The command uname -a also provides the kernel name, network host name, Linux kernel version and its release, release date, hardware name, processor type, hardware platform, and operating system name.

## Command top

The top command provides a dynamic system view. When the top command is executed, a report divided into two parts is dynamically generated. The first part displays statistics on processes and resource usage, the second part shows a list of running processes. If “top” is executed, the first part of the report is similar to the one in the screenshot below.

> ^9BogoMips is a crude measurement of a processor's throughput calculated by the Linux kernel during its boot.

```
top - 12:58:59 up 8:02, 1 user, load average: 0.01, 0.05, 0.01
Tasks: 228 total, 2 running, 226 sleeping, 0 stopped, 0 killed
%Cpu: 0.7 us, 0.7 sy, 98.7 id, 0.0 wa, 0.0 si, 0.0 st
Mem: 2061512 total, 1173 used, 241 free, 25 buff, 598 cache
Swap: 974 total, 61 used, 913 free
```

## 378 Performance, Reliability, and Availability Evaluation of Computational Systems

> ^9BogoMips is a crude measurement of a processor's throughput calculated by the Linux kernel during its boot.


```
├─2*[dbus-daemon]
├─dbus-launch
├─irqbalance
├─login──bash
├─lvmetad
├─mdm──mdm──Xorg──3*[{Xorg}]
│       └─mdmwebkit──┬─{dconf worker}
│                    ├─{gdbus}
│                    ├─{gmain}
│                    ├─12*[{mdmwebkit}]
│                    └─{pool}
├─ntpd
├─polkitd──┬─{gdbus}
│          └─{gmain}
├─rsyslogd──┬─{in:imklog}
│           ├─{in:imuxsock}
│           └─{rs:main Q:Reg}
├─rtkit-daemon──2*[{rtkit-daemon}]
├─sshd──sshd──sshd──bash──pstree
├─2*[systemd──(sd-pam)]
├─systemd-journal
├─systemd-logind
├─systemd-udevd
├─thermald──{thermald}
├─udisksd──┬─{cleanup}
│          ├─{gdbus}
│          ├─{gmain}
│          └─{probing-thread}
└─upowerd──┬─{gdbus}
           └─{gmain}
```

The following pstree command shows our system’s process hierarchy for Linux Mint multi-user.target output on a CUI system like a server.

```
$ pstree
systemd──ModemManager──┬─{gdbus}
                        └─{gmain}
├─NetworkManager──dhclient
│                  └─dnsmasq
│                     ├─{gdbus}
│                     └─{gmain}
├─agetty
├─avahi-daemon──avahi-daemon
├─cgmanger
├─cron
├─cups-browsed──┬─{gdbus}
│               └─{gmain}
├─cupsd
├─dbus-daemon
├─gpg-agent
├─irqbalance
├─mdadm
├─ntpd
├─polkitd──┬─{gdbus}
│          ├─{gmain}
│          └─{pool}
├─rsyslogd──┬─{in:imklog}
│           ├─{in:imuxsock}
│           └─{rs:main Q:Reg}
└─sd_cicero──sd_cicero
```

```
├─{sd_cicero}
│ └─{threaded-m1}
├─sd_dummy──{sd_dummy}
│ └─{threaded-m1}
├─sd_espeak──3*[{sd_espeak}]
│ └─{threaded-m1}
├─sd_generic──{sd_generic}
│ └─{threaded-m1}
├─speech-dispatch──{speech-dispatch}
├─sshd──sshd──sshd──bash──pstree
├─systemd-journal
├─systemd-logind
├─systemd-udevd
└─vsftpd

$
```

Further analysis of the output of the two commands mentioned previously shows that the user is using the system through an Secure Shell (SSH) session and is currently using Bash to run the pstree command.

## 10.7.2.1  ps versus pstree

You can use the ps -auf command to display the parent–child relationship between processes. However, the output for this command is not as complete and fancy as it is for the pstree command, as can be seen in the following session. The ps -uf command displays the process hierarchy for the current user.

```
$ ps -auf
USER       PID %CPU %MEM      VSZ    RSS TTY      STAT START    TIME COMMAND
sarwar   29016  0.0  0.0    23160   5400 pts/0    Ss   07:38   0:00 -bash
sarwar   29127  0.0  0.0    37680   3340 pts/0    R+   07:47   0:00 \\_ ps -auf
root     10096  5.9  6.0   888264 490852 tty7     Sl+  Jul25 6817:12 /usr/lib/xorg/
root      5015  0.0  0.0    16256      0 tty2     Ss+  Jul24  0:00 /sbin/agetty --
root     22407  0.0  0.0   104912   3692 tty1     Ss   Jul24  0:00 /bin/login --
root     12694  0.0  0.0    23160   5152 tty1     S+   Jul25  0:00 \\_ -bash
root      3191  0.0  0.0    16256      0 tty5     Ss+  Jul21  0:00 /sbin/agetty --
root      3187  0.0  0.0    16256      0 tty4     Ss+  Jul21  0:00 /sbin/agetty --
root      3180  0.0  0.0    16256      0 tty3     Ss+  Jul21  0:00 /sbin/agetty --
$ ps -uf
USER       PID %CPU %MEM      VSZ    RSS TTY      STAT START    TIME COMMAND
sarwar   29016  0.0  0.0    23160   5400 pts/0    Ss   07:38   0:00 -bash
sarwar   29130  0.0  0.0    37680   3388 pts/0    R+   07:48   0:00 \\_ ps -uf
$
```

You can run the ps -aflx | more command to display information about all the processes running on your system and some of their important attributes, including PID, PPID, priority, nice value, virtual size, size currently in main memory, status, event waiting for, and full command name used to start the process.

# Exercise 10.16

Run the pstree, ps -auf, and ps -uf commands on your system. Show outputs of these commands. Identify the process on your system that take the highest percentage of CPU time. Also identify the process that uses highest percentage of main memory. Clearly state the amount of virtual memory and physical memory this process is using.

## 10.8  The proc Filesystem

It is instructive to know how to look at, assess, and even change characteristics of the RT operation of the Linux kernel. For example, seeing what processes are running, and what characteristics these processes

have, and then taking actions based upon these observations. A key component of this interaction is the /proc filesystem, often referred to simply as proc. Here we give a brief overview of proc, and show how an understanding of it contributes to helping you in assessing the tasks that Linux manages on your computer. Those tasks are traditionally, and very commonly, referred to as processes and threads.

The proc filesystem is historically derived from the Plan 9 distributed operating system, developed at Bell Labs between the mid-1980s to 2002. This operating system was designed based on most of the principles of UNIX. It glues almost all computing resources, including files, network interfaces, and peripheral devices, through the file system. proc makes it easy for an ordinary user to gain access to kernel data structures, memory allocation, and information about processes on the system. The Linux version of the ps command directly accesses proc to show information about processes on the system. The proc filesystem is mounted at /proc, which gives you the ability to navigate through its hierarchy with the cd command.

The /proc directory structure on our Linux Mint system includes subdirectories for all running processes and other attendant facilities. For all processes on the system, there is a directory named /proc/PID, where PID is the process ID number for any particular process. In that directory, there are numerous files and subdirectories with information about that process. For example, directory 1 is for systemd (PID 1). In the following session, we show commands that gave us information about the systemd process (PID 1).

```
$ cd /proc
$ ls
1 13 22659 29157 49 847 bus misc
10 15 22662 29158 5 85 cgroup groups
100 16 2280 3 50 86 cmdline consoles mtrr
10086 17 22825 30 5015 87 crypto net
10093 177 23 31 51 88 cpuinfo pageinfo
101 179 2306 315 52 884 crypto
10110 18 25 317 53 89 devices partitions
[Output truncated]
```

```
$ cd 1
$ ls
cannot read symbolic link 'cwd': Permission denied
cannot read symbolic link 'root': Permission denied
cannot read symbolic link 'exe': Permission denied
attr cpuset limits net projid_map stat
auxv cwd loginuid ns root statm
cgroup envrion map_files numa_maps sched schedstat syscall
clear_refs fd mem oom_adj session task
cmdline f dinfo mountinfo oom_score_adj setgroups timers
comm gid_map mounts page map smaps uid_map
coredump_filter io mountstats personality stack wchan
```

```
$ sudo ls -la exe
password for bob: xxxxx
lrwx------ 1 root root 0 Jul 24 09:03 exe -> /lib/systemd/systemd
```

```
$ ls -1 /lib/systemd/systemd
-rwxr-xr-x 1 root root 1573136 Apr 12 2016 /lib/systemd/systemd
```

```
$ file /lib/systemd/systemd
/lib/systemd/systemd: ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 2.6.32,
BuildID[sha1]=80c38f5ef6fd5a367d6b043d91b43b11dce9f1fb, stripped
```

```
$ more cmdline
```

```
$ ls -al cmdline
-r--r--r-- 1 root root 0 Jul 25 02:15 cmdline
```

The ls command in the preceding session shows the subdirectories of proc for our purposes here, the running process “numbered” directories. Changing to the 1 directory (the systemd directory), we use the ls command to see the contents of this directory and find out that we have cwd, root, and exe files.

The exe file is a symbolic link to the /lib/systemd/systemd file that contains the executable program that creates systemd. If you have superuser privileges, you can use the su ls -la exe command to verify this information. We then use the ls -la command to find the command line file that originally starts the systemd process. Using the more command to examine the contents of the cmdline file, we see it as a symbolic link to /sbin/init splash, the command that begins the execution of the systemd program.

In addition, there are numerous other subdirectories and files in /proc, which can be queried by Python for example, to extract kernel-related and other values from. Some of those are seen in the outputs of the commands in the previous session. For more in-depth information on the /proc filesystem, and the files and directories in /proc/PID, for example, see the man page for procfs on your Linux system. For more information on systemd, see Chapter 18.

# Exercise 10.17

Replicate the Bash sessions discussed in this section on your system. Do the commands produce expected outputs? How are outputs of the various commands different on your system?

# Summary

A process is a program in execution. Being a time-sharing system, Linux allows execution of multiple processes simultaneously. On a computer system with one CPU, processes are executed concurrently by scheduling the CPU time and giving it to each process for a short time called a quantum. Each process is assigned a priority by the Linux system, and when the CPU is available, it is given to the process with the highest priority.

The shell executes commands by creating child processes using the fork and exec system calls. When a process uses the fork system call, the Linux kernel creates an exact main memory image of the process. The shell itself executes an internal command. An external binary command is executed by the child shell overwriting itself by the code of the command via an exec call. For an external command comprising a shell script, the child shell executes the commands in the script file one by one.

Every Linux process has several attributes, including PID, PPID, process name, process state (running, suspended, swapped, zombie, etc.), the terminal the process was executed on, the length of time the process has run, and process priority. The ps command may be used to view a static display of these attributes. The top command may be used to view a dynamic display of the various system statistics and attributes of the processes running on the system, and permit interactive commands via various keystrokes.

Linux processes can be run in the background or the foreground. A foreground process controls the terminal until it finishes, so the shell cannot be used for anything else while a foreground process runs. When a process runs in the background, it returns the shell prompt so that the user can do other work as the process executes. Because a background process runs at a lower priority, a command that takes a long time is a good candidate for background execution. The background system processes that provide various services are called daemons. A set of commands can be run in a group as separate processes or as one process. Multiple commands can be run from one command line as separate processes by using a semicolon (;) as the command separator; enclosed in parentheses, these commands can be executed as one process. Commands can be executed concurrently by using an ampersand (&) as the command separator.

Suspending processes, moving them from the foreground to the background and vice versa, having the ability to display their status, interrupting them via signals, and terminating them are all known as job control, and Linux has a set of commands that allow these actions. Foreground processes can be suspended and moved to the background pressing <Ctrl+Z> followed by executing the bg command. Suspended and background processes can be moved to the foreground by using the fg command. Commands that are suspended or run in the background are also known as jobs. The jobs command can be used to view the status of all your jobs. You can press <Ctrl+C> to terminate a foreground process.

The kill command can terminate a process with its PID or job ID. The command can be used to send various types of signals, or software interrupts, to processes. Upon receipt of any signal except one,

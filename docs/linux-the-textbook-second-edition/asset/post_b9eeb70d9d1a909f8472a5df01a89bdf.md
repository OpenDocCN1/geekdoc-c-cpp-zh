
# FIGURE 10.2 Process creation via the fork system call.

Step 1: Shell uses fork to create a child

Step 2: Child uses exec to overwrite itself with the executable file corresponding to the sort command.

Step 3: Sort starts execution while 'bash' waits for the command to finish. When sort finishes, the child process terminates and 'bash' starts execution again, waiting for the user to give it another command to execute.

# FIGURE 10.3 Steps for execution of a binary program sort by a Linux shell.

For executing an external binary command, a mechanism is needed that allows the child process to become the command to be executed. The Linux system call exec() can be used to do exactly that, allowing a process to overwrite itself with the executable code for another command. A shell uses the fork() and exec() calls in tandem to execute an external binary command. Figure 10.3 shows the sequence of events for the execution of an external command sort, whose code is in a binary file, /usr/bin/sort.

The execution of a shell script (a series of shell commands in a file; see Chapters 12 and 13) is slightly different from the execution of a binary command/file. In the case of a shell script, the current shell creates a child shell and lets the child shell execute commands in the script file, one by one. Each command in the script file is executed in the same way that commands from the keyboard are; that is, the child shell creates a child for every command that it executes. While the child shell is executing commands in the script file, the parent shell waits for the child to terminate. When the child shell hits the eof marker in the script file, it terminates. The only purpose of the child shell, like any other shell, is to execute commands, and eof means "no more commands." When the child shell terminates, the parent shell comes out of the waiting state and resumes execution. This sequence of events is shown in Figure 10.4, which also shows the execution of a find command in the script file.

Unless otherwise specified in the file containing the shell script, the child shell has the type of the parent shell. That is, if the parent is Bash, the child is also Bash. Thus, by default the shell script is executed by a "copy" of the parent shell. However, a shell script written for any shell (C, TC, Bourne, Bash, Korn, etc.) can be executed regardless of the type of the current shell. To do so, simply specify the type of the child shell under which the script should be executed in the first line of the file containing the shell script as #!full-path-name-of-the-shell. For example, the following line dictates that the child shell is Bash, so the script following this line is executed under the Bash.

```
#!/bin/bash
```

Also, you can execute commands in another shell by running that shell as a child of the current shell, executing commands under it, and terminating the shell. A child shell is also called a subshell. Recall that the commands to run various shells are sh for the Bourne shell, csh for the C shell, tcsh for the TC

![](img/2a18e06cd9c6395e451f26126ecba1fd_265_0.png)

![](img/2a18e06cd9c6395e451f26126ecba1fd_265_1.png)

# FIGURE 10.4 Steps for execution of a shell script by a Linux shell.

shell, ksh for the Korn shell, and bash for Bash. To start a new shell process, simply run the command corresponding to the shell you want to run. See Table 2.4 for a complete path to common Linux shells. If a shell is not installed on your Linux by default, ask your system administrator to install it for you or see Appendix A for instructions to install it on your system. Bash is the default shell on Linux Mint.

In the following session, we are running Bash as the default shell (see Chapter 2, Section 2.8.3, for information on how to set the default shell for the current session, or any subsequent sessions), and the Bourne shell runs as its child. The echo command is executed under the Bourne shell. Then another Bash shell is started, and the echo command is executed under it. The ps command shows the three shells running. Finally, both the TC and Bourne shells are terminated when <Ctrl+D> is pressed in succession, and control goes back to the original shell, Bash. The first <Ctrl+D> terminates the TC shell, giving control back to the Bourne shell. You can also exit a shell running the exit command. Figure 10.5 illustrates all the steps involved, showing the parent–child relationship between processes.

```
$ ps
  PID TTY        TIME CMD
14738 pts/0    00:00:00 bash
14760 pts/0    00:00:00 ps
$ /bin/sh
$ echo "This is Bourne shell."
This is Bourne shell.
$ bash
$ echo "This is Bourne Again SHell."
This is Bourne Again SHell.
$ ps
  PID TTY        TIME CMD
14738 pts/0    00:00:00 bash
14761 pts/0    00:00:00 sh
14762 pts/0    00:00:00 bash
14764 pts/0    00:00:00 ps
$ <Ctrl+D>
$ exit
$ <Ctrl+D>
$
```

# Exercise 10.3

Repeat the previous session on your system to understand how shell processes are created and terminated. Draw the process hierarchy for the output of the last ps command.

![](img/2a18e06cd9c6395e451f26126ecba1fd_266_0.png)

![](img/2a18e06cd9c6395e451f26126ecba1fd_267_0.png)

# FIGURE 10.5 Execution of commands under the child shell (also called subshells).

## 10.5 Process Attributes

Every Linux process has several attributes, including owner ID (called user ID [UID] in Linux jargon), process ID (PID), PID of the parent process (PPID), process name, process state, command executed to start the process, priority of the process, process start time, percentage of the CPU time consumed by the process, percentage of the main memory consumed by the process, size of the process in virtual memory, size of the process currently in main memory, state of the process, the event a process is waiting for (in case it is not running), and the length of time the process has been running. From the user’s and programmer’s point of view, one of the most useful of these attributes is the PID, which is used as a parameter in several process control commands discussed later in this chapter.

Linux provides several tools that allow you to monitor the attributes of the processes currently running on your system, change the states of your processes, and perform various operations on them, including stopping/restarting them, sending them specific messages, having them communicate with each other, and terminating them. In this chapter, we will discuss some of the commands and tools that allow us to monitor the attributes of processes statically and dynamically, as well as perform various operations on processes just stated.

### 10.5.1 Static Display of Process Attributes

The ps command can be used to view a snapshot of the attributes of processes currently in the system. The following is a brief description of the ps command, with option/feature variants for both Berkeley Software Distribution (BSD)-style options (executed without a dash on the command line) and UNIX/POSIX-style options (executed with a dash on the command line).

```
Syntax:
  ps [options]
Purpose: Report static (one shot) information about process status/attributes
Output: A header line and a snapshot of the attributes of processes running on the system.
  Note: Gnu long options are preceded by two dashes.
Commonly used options/features (BSD variants without a preceding dash):
  o    Display information about the comma- or space-separated keywords after the PID field in the default output. You can assign the header of your choice for a keyword by putting an = after the keyword, followed by the header value.
```

- u Display information about the processes for the users specified in the comma-separated list of usernames; no spaces before or after the commas
- a Lift the BSD-style “only yourself” restriction
- e Display the environmental information for each process
- o Similar to -o, except that it does not show the default fields and you can change header texts for multiple using multiple -o options. If no headers are specified with keywords, the header line is not displayed.
- u Display for each process information about the following keywords: user, pid, %cpu, %mem, vsz, rss, tty, state, start, time, and command.
- x Display information about processes that do not have controlling terminals (including daemons)

# Commonly used options/features (UNIX/POSIX variants with a preceding dash):

- -A Select all processes
- -e Same as the -A option: display information about all processes, including session leaders
- -f Display a full format listing, including process owner ID (UID), PID, PPID, C, process start time (STIME), TTY, time executed for (TIME), full command line (CMD)
- -l Display a long listing: F, state (S), UID, PID, PPID, C, PRI, NI, ADDR, SZ, WCHAN, TTY, TIME, CMD
- -u or -U Display a list of processes belonging to UIDs or lognames listed in the comma-separated list

The output of the ps command is sorted first by the terminals associated with processes and then by their PIDs. You can change the default sort order by using different options. If multiple such options are specified, the command exercises the last option. The shell sessions in this section demonstrate the use of the ps command with and without options. We ran all of them on a Linux machine running the Bash shell.

The output of the ps command, as shown in the following session, displays four fields about processes, whose attributes are displayed one per line: PID, the terminal the process is attached to (TTY), the CPU time the process has consumed (TIME), and the command used by the user to run the process (CMD). The output shows that two processes are attached to terminal 0: bash (the login Bash) and ps. The PIDs of the processes attached to terminal 0, -bash and ps, are 27753 and 27783, and have run for 0 s each, respectively.

```
$ ps
PID TTY          TIME CMD
27753 pts/0    00:00:00 bash
27783 pts/0    00:00:00 ps
$
```

You can also add columns of displayed output with the -o option. A comma-separated list must follow the option, with keywords designating which output format columns you want displayed. For example, the following command displays the default columns of output, plus a column showing the state of the processes shown.

```
$ ps -o pid,tty,stat,time,cmd
PID TT  STAT      TIME CMD
27753 pts/0  Ss   00:00:00 -bash
27794 pts/0  R+   00:00:00 ps -o pid,tty,stat,time,cmd
$
```

The state of a process is displayed as a character string—for example, Ss, S+, and R+ in the previous session. Table 10.2 explains the various characters in the string listed under the process state (STAT) column. Thus, the process with the Ss state is a session leader process that is currently sleeping—that is, waiting for less than 20 s. Similarly, the process with the S+ state is a foreground process that has been

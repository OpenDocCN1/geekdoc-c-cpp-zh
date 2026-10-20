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

![](bbox=[0.15, 0.12, 0.85, 0.35])
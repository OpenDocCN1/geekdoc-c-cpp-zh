# Exercise 13.12

After finishing the steps in Exercise 13.10, what happens when you type commands at the shell prompt? Does the result make sense to you? Write the command needed to bring your environment back to normal.

# Exercise 13.13

Create a file that contains the diff2 script and try it with different inputs.

# 13.8 Debugging Shell Scripts

You can debug your Bash scripts by using the -x (echo) option of the sh command. This option displays each line of the script after variable substitution but before its execution. You can combine the -x option with the -v (verbose) option to display each line of the script, as it appears in the script file, before execution. You can also invoke the sh command from the command line to run the script, or you can make it part of the script, as in #!/bin/sh -xv. In the latter case, remove the -xv options after debugging is complete.

```
cat debug_demo
#!/bin/bash
echo -e "Enter a digit: \c"
read var1
if ["$var1" -ge 1 -a "$var1" -le 9 ]
then
echo "Good input!"
exit 0
```

In the following session, we show how a shell script can be debugged. The script in the debug_demo file prompts you for a digit. If you enter a value between 1 and 9, it displays Good input! and quits. If you enter any other value, it simply exits. When the script is executed and you enter 4, it displays the message ./debug_demo: line 9: syntax error: unexpected end of file. This message usually means that you have not completely closed out a control construct such as missing fi in an if statement or missing done in a while statement.

```
$ cat debug_demo
#!/bin/bash
echo -e "Enter a digit: \c"
read var1
if ["$var1" -ge 1 -a "$var1" -le 9 ]
then
echo "Good input!"
exit 0

$ ./debug_demo
Enter a digit: 4
./debug_demo: line 9: syntax error: unexpected end of file
$
```

We debug the program by using the sh -xv debug_demo command. The error message clearly states that fi in the if statement is missing. We insert fi at the rightful place and rerun the program. We now get the error message ./debug_demo: 5: debug_demo: [4: not found. The shaded portion of the run-time trace shows the problem area. In this case, the error is generated because of a problem of the condition for the if statement. A closer examination of the shaded area reveals that a missing space between [ and 4 is the problem. In other words, the comparison between [4 and 1 is the problem; it should be between 4 and 1. After we take care of this problem by changing ["$var1" to [ "$var1", the script works properly.

```
$ sh -xv debug_demo
#!/bin/bash
echo -e "Enter a digit: \c"
+ echo -e "Enter a digit: \c"
read var1
+ read var1
4
if ["$var1" -ge 1 -a "$var1" -le 9 ]
then
echo "Good input!"
exit 0
```
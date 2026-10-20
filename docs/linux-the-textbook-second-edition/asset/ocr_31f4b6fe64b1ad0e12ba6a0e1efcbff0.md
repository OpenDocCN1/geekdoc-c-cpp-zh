already exists, it is overwritten; otherwise, it is created. The following example shows how the standard error of ls -l can be redirected to a file.

```
$ ls -l foo 2> error.log
... long listing for foo if no errors ...
$
```

The output of ls -l foo goes to the display screen, and error messages go to error.log. Thus, if foo does not exist, the error message ls: foo: No such file or directory goes into the error.log file, as shown in the following session. The actual wording of the message varies from system to system, but it basically informs you that foo does not exist.

```
$ ls -l foo 2> error.log
$ cat error.log
ls: foo: No such file or directory
$
```

Keeping standard error attached to the display screen and not redirecting it to a file is useful in many situations. For example, when the cat lab1 lab2 lab3 > a11 command is executed to concatenate files lab1, lab2, and lab3 into a file called a11, you would want to know whether any of the three input files are nonexistent or if you do not have permission to read any of them. In this case, redirecting the error message to a file does not make much sense because you want to see the immediate results of the command execution.

# 9.8 Redirecting stdout and stderr in One Command

Standard output and standard error can be redirected to the same file. One obvious way to do so is to redirect stdout and stderr to the same file by using file descriptors with the > symbol, as in the following command.

```
$ cat lab1 lab2 lab3 1> cat.output 2> cat.errors
$
```

In this case, the input of the cat command comes from the lab1, lab2, and lab3 files, its output goes to the cat.output file, and any error message goes to the cat.errors file, as shown in Figure 9.7.

![](bbox=[0.16, 0.68, 0.88, 0.9])

FIGURE 9.7 Error redirection: (a) file descriptors and standard files for cat lab1 lab2 lab3 1> cat.output 2> cat.errors; (b) semantics of the cat command.
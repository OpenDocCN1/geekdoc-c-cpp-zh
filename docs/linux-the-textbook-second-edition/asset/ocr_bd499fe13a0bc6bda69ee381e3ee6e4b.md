![](bbox=[0.15, 0.12, 0.85, 0.31])

FIGURE 9.8 Error redirection: (a) file descriptors and standard files; (b) semantics of the cat lab1 lab2 lab3 1> cat.output.errors 2>&1 and cat lab1 lab2 lab3 2> cat.output.errors 1>&2 commands.

Note that, although not shown in Figure 9.7b, files lab1, lab2, and lab3 have file descriptors assigned to them when they are opened for reading by the cat command. The command produces an error message if any one of the three “lab” files does not exist or if you do not have read permission for any of these files.

The following command redirects the stdout and stderr of the cat command to the cat.output.errors file. Thus, the same file (cat.output.errors) contains the output of the cat command, along with any error messages that may be produced by the command.

```
$ cat lab1 lab2 lab3 1> cat.output.errors 2>&1
$
```

In this command, the string 2>&1 tells the command shell to make descriptor 2 a duplicate of descriptor 1, resulting in the error messages going to the same place that the command output goes to. Similarly, the string 1>&2 can be used to tell the command shell to make descriptor 1 a duplicate of descriptor 2. Thus, the following command accomplishes the same task. Figure 9.8 shows the semantics of the two commands.

```
$ cat lab1 lab2 lab3 2> cat.output.errors 1>&2
$
```

The evaluation of the command line content for file redirection is left to right. Therefore, redirections must be specified in the left-to-right order if one notation is dependent on another. In the preceding command, first, stderr is changed to the file cat.output.errors, and then stdout becomes a duplicate of stderr. Thus, the output and errors for the command both go to the same file, cat.output.errors.

The following command therefore does not have the effect of the two commands just discussed. The reason is that, in this command, stderr is made a duplicate of stdout before output redirection. Therefore, stderr becomes a duplicate of stdout (the display screen at this time) first, and then stdout is changed to the file cat.output.errors. Thus, the output of the command goes to cat.output.errors and errors go to the display screen. The sequence shown in Figure 9.9 illustrates the semantics of this command.

```
$ cat lab1 lab2 lab3 2>&1 1> cat.output.errors
$
```

Note that Figure 9.9a and b are identical because the execution of cat lab1 lab2 lab3 2>&1 does not make any changes to stdout and stderr—they stay attached to the display screen before and after the command is executed.
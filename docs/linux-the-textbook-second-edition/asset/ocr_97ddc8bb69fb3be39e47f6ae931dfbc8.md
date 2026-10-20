![](bbox=[0.327, 0.096, 0.673, 0.417])

**FIGURE 13.5**  Detachment and reattachment of **stdin** and **stdout** inside a shell script.

```
cat > file3
exec < /dev/tty
cat > file4
$ ./exec.demo1
Hello, world!
<Ctlr+D>
This is great!
<Ctlr+D>
$ more file1
Hello, world!
$ more file2
Contents of file2.
$ more file3
Contents of file2.
$ more file4
This is great!
$
```

Now, we develop a shell script, diff2, which uses the file input/output (I/O) features of Bash. It takes two files as command line arguments and compares them line by line. If the files are the same, it displays a message that says so, and the program terminates. If one file is smaller than the other, it displays a message informing you of that and exits. As soon as the program finds the lines at which the two files differ, it displays an error message informing you of the lines from both files that are different and terminates. The following is the script and a few sample runs:

```
$ cat diff2
#!/bin/bash
# File Name: ~/linux2e/chap13/bash/diff2
# Author:     Syed Mansoor Sarwar
# Written:    August 28, 2004
# Modified:   July 29, 2014; April 9, 2017
# Purpose:    To see if the two files passed as command line arguments
#            are same or different
```
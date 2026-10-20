![](bbox=[0.32, 0.09, 0.58, 0.57])

FIGURE 9.16 Semantics of the cat names students | grep "John Doe" | tee file1 file2 | wc -l command.

```
% ls -l foo >& error.log
%
```

The TC shell does not have an operator to redirect stderr alone. However, the stdout and stderr of a command can be attached to different files, if the command is executed in a subshell, by enclosing the command in parentheses. The following session illustrates this point.

```
% find ~ -name foo -print >& output.error.log
% (find ~ -name foo -print > foo.paths) >& error.log
%
```

The children of your current shell process, also known as subshells (see Chapter 10), execute all external shell commands. When the first command executes, the output and errors of the find command go to the output.error.log file. Because the subshell process is not created until the whole command line has been processed (interpreted), the stdout and stderr of the parent shell process are redirected to the error.log file because of the >& operator. Therefore, the subshell also has its stdout and stderr redirected to the error.log file.

In the second command line, the find command is executed under a subshell and inherits the standard files of the parent shell. When the find command in parentheses executes, it redirects the stdout of the
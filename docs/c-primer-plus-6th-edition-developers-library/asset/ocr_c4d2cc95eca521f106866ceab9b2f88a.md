(Unix) or Ctrl+Z (DOS) at the beginning of a line. Try it. If you can’t think of anything to type, just imitate the next example. In it, we use the $ Unix prompt. Remember to end each line by pressing Enter to send the buffer contents to the program.

```
$ echo_eof > mywords
You should have no problem recalling which redirection
operator does what. Just remember that each operator points
in the direction the information flows. Think of it as
a funnel.
[Ctrl+D]
$
```

After the Ctrl+D or Ctrl+Z is processed, the program terminates and your system prompt returns. Did the program work? The Unix ls command or Windows Command Prompt dir command, which lists filenames, should show you that the file mywords now exists. You can use the Unix and Linux cat or DOS type command to check the contents, or you can use echo_eof again, this time redirecting the file to the program:

```
$ echo_eof < mywords
You should have no problem recalling which redirection
operator does what. Just remember that each operator points
in the direction the information flows. Think of it as a
funnel.
$
```

# Combined Redirection

Now suppose you want to make a copy of the file mywords and call it savewords. Just issue this next command,

```
echo_eof < mywords > savewords
```

and the deed is done. The following command would have worked as well, because the order of redirection operations doesn’t matter:

```
echo_eof > savewords < mywords
```

Beware: Don’t use the same file for both input and output to the same command.

```
echo_eof < mywords > mywords....<--WRONG
```

The reason is that > mywords causes the original mywords to be truncated to zero length before it is ever used as input.

In brief, here are the rules governing the use of the two redirection operators (< and >) with Unix, Linux, or Windows/DOS:

+   A redirection operator connects an executable program (including standard operating system commands) with a data file. It cannot be used to connect one data file to another, nor can it be used to connect one program to another program.
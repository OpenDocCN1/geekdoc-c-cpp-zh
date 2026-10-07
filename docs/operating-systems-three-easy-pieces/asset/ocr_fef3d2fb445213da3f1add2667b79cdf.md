# INTERLUDE: FILES AND DIRECTORIES

> TIP: USE TRACE (AND SIMILAR TOOLS)
The trace tool provides an awesome way to see what programs are up to. By running, you can trace what system calls a program makes, see the arguments and return codes, and generally get a very good idea of what is going.
The tool also takes arguments that can be quite useful. For example, -f foo for children too; -t reports the time of day at each call; -e trace=open,close,read,write traces to those system calls and ignores all others. There are many other flags; read the main pages and find out how to harness this wonderful tool.

# 39.4 Reading And Writing Files

Once we have some files, course we might like to read or write them. Let's start by reading an existing file. If we were typing at a command line, we might just use the program cat to dump the contents of the file to the screen.

```
prompt> echo hello foo
prompt> cat foo
hello
prompt>
```

In this code snippet, we redirect the output of the program echo to the file foo, which contains the word "hello" in it. We then use cat to see the contents of the file. But how does the cat program access the file?\ To find this we'll use an incredibly useful tool to trace the system calls made by a program. On Linux, the tool is called trace; other systems have similar tools like dtruss on a Mac, or truss on other Unix variants. What trace does is trace every system call made by a program while it runs, and dump the trace to the screen for you to see. Here is an example of using trace to find out what cat is doing (some calls removed for readability):

```
prompt> cat foo
...
open("foo", O_LARGEFILE) = 3
read(3, "hello\n", 4096) = 6
write(1, "hello\n", 6) = 6
hello
read(3, "", 4096) = 0
close(3) = 0
...
prompt>
```

© 2008–19, ARPAC-DUSSEAU
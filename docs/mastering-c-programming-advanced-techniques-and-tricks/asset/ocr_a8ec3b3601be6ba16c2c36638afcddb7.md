# Reverse Debugging

One of the more powerful, but underutilized, features of gdb is reverse debugging. This allows you to step backwards in the execution of your program, which is invaluable when you’ve overshot the problematic part of your code.

To enable reverse debugging, start gdb with the --record flag. For instance, to debug a program called you would launch gdb as follows:

```
gdb --args ./my_program --record
```

Then, you can use commands like reverse-step or reverse-continue to navigate backwards through the program’s execution.
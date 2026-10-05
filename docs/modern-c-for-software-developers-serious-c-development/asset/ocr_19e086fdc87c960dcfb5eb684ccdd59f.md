Note: break at a scoped function by using the scope resolution operator, for example:

```
gdb> b account : :balance
```

We can delete all of the breakpoints with:

```
gdb> delete
or
gdb> d
```

A particular breakpoint can be deleted with:

+   * gdb> clear [line number]
* gdb> clear [function_name]

We can get information on all of the breakpoints with:

```
gdb> info
```

Note: the GDB debugger can be used to debug threads.

# Saving Breakpoints Between Debugging Sessions

If you are engaged in a complex debugging session, you will most likely have set up multiple breakpoints in a number of source files. Furthermore it will most likely take than one debugging session to locate the bug. In such a situation it is completely frustrating as well as time consuming to have up the breakpoints whenever you start a new session. GDB provides a way to avoid this problem.

Firstly set up your breakpoints in the normal manner. Then save your breakpoints to a file:

```
gdb> save breakpoints breakpoints.txt
```
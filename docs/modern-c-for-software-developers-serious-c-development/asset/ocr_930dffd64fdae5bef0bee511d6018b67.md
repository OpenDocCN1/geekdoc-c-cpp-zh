```
gdb> l filename:line_number
```

We can list a few lines of a function with:

```
gdb> l function_name
```

# Continuing The Debugging Session

After we have examined the code at a breakpoint, we can continue the debugging session with:

```
gdb> continue          (or gdb> c)
or
gdb> continue repeat count
```

If we just press the return key by itself gdb will repeat the previous command.

# Restarting A Debugging Session

We can restart an entire debugging session with:

```
gdb > restart
```

# Examining And Setting Variables

When we are at a breakpoint, we can examine a variable such as foo with:

```
gdb> print foo
or
gdb> p foo
```
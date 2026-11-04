how the lock is acquired and released. The CLR doesn't have those primitives inside the IL instruction set, so BCL calls have to be used to realize this. The whole picture is shown in Figure 8.30.

![](bbox=[0.1, 0.23, 0.6, 0.7])

FIGURE 8.30 The lock statement unraveled.

The portion wrapped in the big curly braces is the compiled code from inside the lock statement's code block. The rest of the code is what the lock statement itself is responsible for and essentially boils down to a call to Monitor.Enter before executing the code and one to Monitor.Leave inside the finally clause to be guaranteed it runs for sure, even if an exception is thrown during the execution of the block.

Those primitives from the System.Threading namespace can be called manually, as well, if you want. More Monitor methods exist to accommodate a variety of scenarios (for example, if you want to wait to acquire a lock only for a specified duration). If that timeout is exceeded, you could go on to do something else and attempt to acquire the lock again at some later point.

# Intermezzo: Code Generation for Lock

In the last release of the C# language, code generation for the lock statement has been changed due to a truly fascinating story in compiler development land. Consider the following fragment:

```
lock (expression)
    embedded-statement
```
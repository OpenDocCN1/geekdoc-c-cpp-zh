![](bbox=[0.087, 0.123, 0.913, 0.417])

**FIGURE 11.1** How Function Arguments and Parameters Are Organized in Memory

*When a function is called, its arguments are copied to the parameters. But if the function changes a parameter, then the change is not seen in the caller. However, if an argument contains the address of a variable, then the corresponding parameter of the argument can be used to change that variable.*

The preceding paragraphs relating to the use of memory addresses provided a gentle introduction to pointers, touted as the strongest feature of C. We’ll unravel the mystery of pointers in Chapter 12, but we’ll encounter the topic in a disguised form when we use arrays as function arguments in Section 11.8.

> **Note:** Even if the changed value of a parameter is not seen by the caller, a function can make it available through the **return** statement. However, a function can return only one value, so you can’t return multiple parameters in this manner.

# 11.5.3 Local Variables

A function has its own set of *local* variables that are defined in its implementation. For instance, the **c2f** function uses a local variable, *fheit*, to compute the result it returns to its caller. Unlike parameters, local variables cannot be assigned by the caller. However, parameters and local variables have the following features in common:

+   - Their names don’t conflict with identical names defined in the caller or any other function.
+   - They can be accessed only in the function they are defined in. They are neither *visible* in the caller nor in any other function.
+   - They last as long as the function is active. This means that they are created every time the function is called.
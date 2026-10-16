without giving the caller of the function that called **exit()** a chance to deal with the problem. It is therefore often best to leave a context by throwing an exception and letting a handler decide what to do next. For example, **main()** may catch every exception (§13.5.2.2).

The C (and C++) standard-library function **atexit()** offers the possibility to have code executed at program termination. For example:

```
void my_cleanup();
void somewhere() {
if (atexit(&my_cleanup)==0) {
// my_cleanup will be called at normal termination
}
else {
// oops: too many atexit functions
}
}
```

This strongly resembles the automatic invocation of destructors for global variables at program termination (§15.4.1, §16.2.12). An argument to **atexit()** cannot take arguments or return a result, and there is an implementation-defined limit to the number of atexit functions. A nonzero value returned by **atexit()** indicates that the limit is reached. These limitations make **atexit()** less useful than it appears at first glance. Basically, **atexit()** is a C workaround for the lack of destructors.

The destructor of a constructed statically allocated object (§6.4.2) created before a call of **atexit(f)** will be invoked after **f** is invoked. The destructor of such an object created after a call of **atexit(f)** will be invoked before **f** is invoked.

The **quick_exit()** function is like **exit()** except that it does not invoke any destructors. You register functions to be invoked by **quick_exit()** using **at_quick_exit()**.
The **exit()**, **abort()**, **quick_exit()**, **atexit()**, and **at_quick_exit()** functions are declared in **<cstdlib>**. 

# 15.5 Advice

[1] Use header files to represent interfaces and to emphasize logical structure; §15.1, §15.3.2. [2] **#include** a header in the source file that implements its functions; §15.3.1. [3] Don’t define global entities with the same name and similar-but-different meanings in different translation units; §15.2.

[4] Avoid non-inline function definitions in headers; §15.2.2.
[5] Use **#include** only at global scope and in namespaces; §15.2.2.
[6] **#include** only complete declarations; §15.2.2.
[7] Use include guards; §15.3.3.

[8] **#include** C headers in namespaces to avoid global names; §14.4.9, §15.2.4. [9] Make headers self-contained; §15.2.3.
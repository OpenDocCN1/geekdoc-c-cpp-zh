accessible. Storage duration and scope (*where a name can be used*) are separate issues, as we’ll see in Section 5.13.

There are several types of identifiers with static storage duration: *external identifiers* (such as global variables and function names) and local variables declared with the storage-class specifier `static`. Global variables and function names have storage class `extern` by default. Global variables are created by placing variable declarations outside any function definition. They retain their values throughout program execution. Global variables and functions can be referenced by any function that follows their declarations or definitions in the file. This is one reason for using function prototypes—when we include `stdio.h` in a program that calls `printf`, the function prototype is placed at the start of our file to make the name `printf` known to the rest of the file.

Defining a variable as global rather than local allows unintended side effects to occur when a function that does not need access to the variable accidentally or maliciously modifies it. In general, you should avoid global variables except in situations with unique performance requirements (as discussed in Chapter 15). Variables used only in a particular function should be defined as local variables in that function.

Local `static` variables are still known only in the function in which they’re defined and retain their value when the function returns. The next time the function is called, the `static` local variable contains the value it had when the function last exited. The following statement declares local variable `count` to be `static` and initializes it to 1:

```
static int count = 1;
```

All numeric values of static storage duration are initialized to zero by default if you do not explicitly initialize them.

Keywords `extern` and `static` have special meaning when explicitly applied to external identifiers. Chapter 15 discusses the explicit use of `extern` and `static` with external identifiers and multiple-source-file programs.

ERR

PERF

# ## Self Check

+   1. **(Fill-In)** Each identifier in a program has attributes, including storage class, storage duration, ________ and ________.
+   
+      **Answer:** scope, linkage.

+   2. **(Multiple Choice)** Which of the following statements a), b) or c) is *false*?
+   
+      a) An identifier’s storage duration is the period during which the identifier exists in memory.
+   
+      b) An identifier’s scope is where the identifier can be referenced in a program.
+   
+      c) Keyword `auto` declares variables of automatic storage duration. Such variables are created when program control enters the block in which they’re defined. They exist while the block is active, and they’re destroyed when program control exits the block.
+   
+      d) All of the above statements are *true*.
+   
+      **Answer:** d.
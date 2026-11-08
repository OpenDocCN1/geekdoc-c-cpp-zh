# Chapter 12

It is a good practice to make use of these macros when we are writing a program. It helps in debugging the program. Consider the following program:

```
```cpp
//Demonstrating the usage of predefined macros in C++
#include<stdio.h>
int main ()
{
    printf("We are in File:[%s] on Line No:[%d] at %s",__FILE__,__LINE__,
           __DATE__,__TIME__);
    return 0;
}
```
```

After executing the preceding program, we get the following output:

```
```text
We are in File:[debugging.c] on Line No:[5] at Mar 16 2012 14:27:54
```
```

The preceding information can help us in debugging large projects consisting of multiple files.

Now, let’s summarize the main points discussed in the chapter.

# Summary

This chapter mainly discussed the basics of programming using the C++ language. We have started the chapter by explaining the structure of a typical C++ program and ended by describing dynamic memory management operators followed by preprocessor directives. In addition, we have explained about the basic data types, expressions, operators, and operator precedence in C++. Further, we have learned about type conversions, arrays, strings, structures and references in C++. We have also discussed about flow control statements and functions, with a special attention to inline and recursive functions.

In the next chapter, we learn about classes and data abstraction in C++.

# Quick Revise

# Multiple Choice Questions

+   **Q1.** What is the entry point of a C++ program?
+   
+   1. `start()`
+   2. `main()`
+   3. First statement in the source code after preprocessor entries
+   4. `program()`
+   5. `system()`

+   **Q2.** What is the correct value to return to the operating system upon the successful completion of a program?
+   
+   1. `-1`
+   2. `1`
+   3. `0`
+   4. Programs do not return a value

+   **Q3.** Which of the following is not a correct variable type in C++?
+   
+   1. `int`
+   2. `float`
+   3. `real`
+   4. `double`
# DISCUSSION QUESTIONS

+   1. Explain the facilities provided by the C preprocessor with examples.
+   2. What is a macro and how is it different from a C variable name?
+   3. What precautions one should take when using macros with argument?
+   4. What are the advantages of using macro definitions in a program?
+   5. When does a preprocessor use `#include` directive?
+   6. The value of a macro name cannot be changed during the running of a program. Comment?
+   7. What is conditional compilation? How does it help a programmer?
+   8. Distinguish between `#ifdef` and `#if` directives.
+   9. Comment on the following code fragment:
+   10. Enumerate the differences between functions and parameterized macros.
+   11. In `#include` directives, some file names are enclosed in angle brackets while others are enclosed in double quotation marks. Why?
+   12. Why do we recommend the use of parentheses for formal arguments used in a macro definition? Give an example.

```
```c
#if 0
{
        line-1;
        line-2;
        ...
        ...
        line-n;
}
#endif
```
```

# DEBUGGING EXERCISES

1. Identify errors, if any, in the following macro definitions:

```
```c
(a) #define until(x) while(!x)

(b) #define ABS(x) (x > 0) ? x : (-x)

(c) #ifdef(FLAG)
        #undef  FLAG
    #endif

(d) #if n = 1 update(item)
        #else print-out(item)
    #endif
```
```

![](bbox=[0.755, 0.179, 0.879, 0.855])
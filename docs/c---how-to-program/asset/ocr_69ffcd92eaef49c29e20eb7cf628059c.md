13.2 Write a program to print the values of the predefined symbolic constants listed in Fig. 13.1.

13.3 Write a preprocessor directive to accomplish each of the following:

+   - a) Define symbolic constant YES to have the value 1.
+   - b) Define symbolic constant NO to have the value 0.
+   - c) Include the header common.h. The header is found in the same directory as the file being compiled.
+   - d) Renumber the remaining lines in the file beginning with line number 3000.
+   - e) If symbolic constant TRUE is defined, undefine it and redefine it as 1. Do not use #ifdef.
+   - f) If symbolic constant TRUE is defined, undefine it and redefine it as 1. Use the #ifdef preprocessor directive.
+   - g) If symbolic constant TRUE is not equal to 0, define symbolic constant FALSE as 0. Otherwise define FALSE as 1.
+   - h) Define macro CUBE_VOLUME that computes the volume of a cube. The macro takes one argument.

# Answers to Self-Review Exercises

13.1 a) #. b) #elif. c) #define. d) whitespace. e) #undef. f) #ifdef, #ifndef. g) Conditional compilation. h) assert. i) #include. j) #. k) #. l) \. m) #line.

13.2 See below. [Note: `__STDC__` works in Visual C++ only with the /Za compiler flag.]

```
```c
1   // Print the values of the predefined macros
2   #include <stdio.h>
3   int main(void)
4   {
5      printf("__LINE__ = %d\n", __LINE__);
6      printf("__FILE__ = %s\n", __FILE__);
7      printf("__DATE__ = %s\n", __DATE__);
8      printf("__TIME__ = %s\n", __TIME__);
9      printf("__STDC__ = %s\n", __STDC__);
10  }
```
```

```
```
__LINE__ = 5
__FILE__ = ex13_02.c
__DATE__ = Jan 5 2012
__TIME__ = 09:38:58
__STDC__ = 1
```
```

+   - a) `#define YES 1`
+   - b) `#define NO 0`
+   - c) `#include "common.h"`
+   - d) `#line 3000`
+   - e)
+     ```c
+     #if defined(TRUE)
+         #undef TRUE
+         #define TRUE 1
+     #endif
+     ```
+   - f)
+     ```c
+     #ifdef TRUE
+         #undef TRUE
+         #define TRUE 1
+     #endif
+     ```
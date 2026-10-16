7.3 In FORTRAN, global variables are created using a COMMON statement, but it is not required that the global variables have the same name in each subroutine or function. Thus, in the code

```
FUNCTION F
COMMON N
---
END

SUBROUTINE S
COMMON M
---
END
```

variable N in function F and variable M in subroutine S share the same memory, so they behave as different names for the same global variable. Compare this method of creating global variables to that of C. How is it better? How is it worse?

7.4 Discuss the advantages and disadvantages of C’s declaration before use rule with C++’s relaxation of that rule to extend the scope of a declaration inside a class declaration to the entire class, regardless of its position in the declaration.

7.5 C++ relaxes C’s rule that all declarations in a block must come at the beginning of the block. In C++, declarations can appear anywhere a statement can appear. Discuss this feature of C++ from the point of view of (a) the principle of locality; (b) language complexity; (c) implementation complexity.

7.6 Describe the bindings performed by a C extern declaration. Why is such a declaration necessary?

7.7 As noted in this chapter, C and C++ make a distinction between a declaration and a definition. Which of the following are declarations only and which are definitions?

+   (a) char * name;
+   (b) typedef int * IntPtr;
+   (c) struct rec;
+   (d) int gcd(int,int);
+   (e) double y;
+   (f) extern int z;

7.8 Using the first organization of the symbol table described in the text (a single simple table), show the symbol table for the following C program at the three points indicated by the comments (a) using lexical scope and (b) using dynamic scope. What does the program print using each kind of scope rule?

```
#include <stdio.h>

int a,b;

int p(){int a, p;
/* point 1 */
```

(continues)
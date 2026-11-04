```
~~~c
#include "FindChar2.h"
~~~
```

This type of “separation” of files with function prototypes and implementation code is analogous to an interface file and an implementation file in Java. Although you probably won’t use it until you have progressed beyond the beginner stage, it’s good to be aware of this functionality.

# # FUNCTION PARAMETERS IN C FUNCTIONS

Function parameters are formal parameters, and they are treated as local variables within the function where they appear. In addition, such parameters take precedence over the global variables.

[Listing 4.1](#) displays the contents of `FunctionParams.c` that illustrates the use of local and global variables in a C program.

***LISTING 4.1: FunctionParams.c***

```
~~~c
#include <stdio.h>

// global variable declaration
int a = 20;

// function to add two integers
int sum(int a, int b)
{
    printf ("value of a in sum() = %d\n",  a);
    printf ("value of b in sum() = %d\n",  b);

    return a + b;
}
~~~
```
this memory location can be identified or accessed later in the program. Such memory spaces which are nameless and unidentifiable are called Rvalues. Remember, after the statement executes value `10` will be present in variable `a` which is accessible later in the program but the temporary space in which `10` was stored during the execution of the statement will no longer be accessible.

Important property of Rvalues is that, they can never be modified as they are constants. The following statement would not make any sense

```
20=10;
```

because `20` is a constant integer value and it cannot appear on the left-hand side of the assignment operator. Compiler gives following error if such statements are written in the program.

```
ERROR: Lvalue required.
```

This means that the value present on the left-hand side of the statement is not Lvalue but an Rvalue which cannot be modified.

# 8.15.1  Creating Lvalue’d function using reference variables (Possible only in C++ and not in C)

Lvalue’d function is a function which can appear as an Lvalue in the expression. Reference variables and pointers both can be used to create Lvalue’d function. In this section, we will implement an Lvalue’d function using reference variables. C programmers can skip this reading and directly read the note given at the end of this section which gives the implementation of Lvalue’d functions using pointers. This is because C does not support reference variables. If you are a C++ programmer, this section will explain you how to create an Lvalue’d function using reference variables.

Consider, the following code which creates a global variable `a` initialized with a value `10` and function `f1()` which increments the value of `a` and returns to function `main()`.

```
#include<stdio.h>
int a=10;
int f1()
{
a++;
return a;
}
void main()
{
f1()=20;
printf("Value of a is %d",a);
}
```

The first statement in `main()`,

```
f1()=20;
```
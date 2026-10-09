```
```
For example:
#include <stdio.h>
#include <stdlib.h>
int *funA(void)
{
    int c = 42;
    return &c;
}

int main(int argc, char **argv)
{
    int *result=funA();
    printf("%d\n",*result);
    return (EXIT_SUCCESS);
}
```
```

In this program funA creates a local variable c and stores 42 in it. It then returns the address of c and the main program uses this to print the value stored in c. In most cases this program will cause the compiler or the IDE to flag the potential error:

![](bbox=[0.1, 0.43, 0.78, 0.56])

The warning message is perfectly correct in that c is a local variable and hence only “lives” while the function is executing, and as such you should not return its address. However, if you run the program there is a good chance you will see 42 printed because the stack where the value of c was stored hasn’t changed. On some systems you will see a runtime error because the stack has changed enough to cause a memory fault. If another function is called after funA and before the value of c is printed then the chances are that you will not see 42, but some other value as stored on the stack by the other function.

This may seem like a contrived example, it is, but it is a far more common error than you might imagine as we will discover in Dive 13: First Class Functions.

The important point is that once a function returns you have to regard all of its local variables and everything it stored on the stack as being destroyed, even though they may hang around for a while simply because some other function hasn’t made use of the memory as yet.
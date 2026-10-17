In the above simple program once the control encounters the caller functions in this case mus() the control directs itself to the called function and executes the statements and executes the printf statement below it and returns to the main. In this case the result of a program would be:

# 5.6.1. My Honey

Functions that accepts parameters but don’t return values. For functions this the caller function transport, some values to the called function or the function definition where these values are used for some specific function or computation but once the computed value is found out within the called function the value is not returned back to the caller function.

The program below should give a clear picture.

+   - **Example:**

```
main()
{
int a,b; printf(“Enter a & b”);
scanf(“%d %d”, &a,&b);
add (a,b);
}
add(intx,inty)
{
int z;
z=x+y;
printf(“a+b=%d”, z);
clrscr();
}
```

In the above event once the values are passed into the called function they are summed up and the total is displayed within the function itself. Functions that takes parameters and returns values In the third & final type of functions the values as the arguments are being passed into the called function where they will be computed and a definite result is relayed back to the caller function and the value will be printed from there. The following things should comprehend things further:

```
#include<stdio.h>
```
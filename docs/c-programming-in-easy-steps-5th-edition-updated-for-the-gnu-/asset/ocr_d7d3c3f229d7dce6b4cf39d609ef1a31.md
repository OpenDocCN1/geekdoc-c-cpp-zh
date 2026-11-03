![](bbox=[0.1, 0.11, 0.22, 0.24])

Many C programmers never use bitwise operators but it is useful to understand what they are and how they may be used.

![](bbox=[0.1, 0.33, 0.22, 0.46])

Each half of a byte is known as a "nibble" (4 bits). The binary numbers in the examples in the table describe values stored in a nibble.

Unless programming for a device with limited resources there is seldom a need to utilize bitwise operators, but they can be useful. For instance, the XOR (eXclusive OR) operator lets you exchange values between two variables without the need for a third variable.

1. Begin a new program with a preprocessor instruction to include the standard input/output library functions

```
#include <stdio.h>
```

![](bbox=[0.1, 0.83, 0.22, 0.92])

xor.c

2. Add a main function that declares and initializes two integer variables, then outputs their initial values

```
int main()
{
int x = 10 , y = 5 ;
printf("\n x=%d y=%d\n", x , y );
}
```

3. Next, in the main function block, insert an XOR statement three times to exchange the variable values by binary bit manipulation
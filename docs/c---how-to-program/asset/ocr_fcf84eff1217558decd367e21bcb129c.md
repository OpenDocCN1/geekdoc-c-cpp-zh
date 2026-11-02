# 4.3 Counter-Controlled Iteration

Counter-controlled iteration requires:

+   1. The name of a control variable (or loop counter).
+   2. The initial value of the control variable.
+   3. The increment (or decrement) by which the control variable is modified each time through the loop.
+   4. The condition that tests for the final value of the control variable (i.e., whether looping should continue).

Consider the simple program shown in Fig. 4.1, which prints the numbers from 1 to 10. The definition

```
unsigned int counter = 1; // initialization
```

names the control variable (counter), defines it to be an integer, reserves memory space for it, and sets its initial value to 1.

```
```c
// Fig. 4.1: fig04_01.c
// Counter-controlled iteration.
#include <stdio.h>

int main(void)
{
    unsigned int counter = 1; // initialization

    while (counter <= 10) { // iteration condition
        printf("%u\n", counter);
        ++counter; // increment
    }
}
```
```

![](bbox=[0.119, 0.625, 0.858, 0.8])

**Fig. 4.1** | Counter-controlled iteration.

The definition and initialization of counter also could have been written as

```
```c
unsigned int counter;
counter = 1;
```
```

The definition is *not* executable, but the assignment is. We’ll use both methods of setting the values of variables.
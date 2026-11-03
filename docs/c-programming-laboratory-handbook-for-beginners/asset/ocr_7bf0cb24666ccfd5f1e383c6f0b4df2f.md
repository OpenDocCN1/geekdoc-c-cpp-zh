repeats until the condition becomes *false*. Because *while* loop checks the condition before the block is executed, the control structure is known as a pre-test loop (entry-controlled loop).

# ## Sample Program: While Loop

# ### Program 1

Program to print the message “Hello” 10 times. This program will give an idea of how while loop works.

```
```c
#include <stdio.h>
void main()
{
    int i=10;
    while (i > 0)
    {
        printf(“Hello\n”);
            i=i - 1;
    }
}
```
```

# ### Sample Output

```
```text
Hello
Hello
Hello
Hello
Hello
Hello
Hello
Hello
Hello
Hello
```
```

# ## Related Theory

The **Euclidean algorithm** (also called **Euclid's algorithm**) is an efficient method for computing the greatest common divisor (GCD), also known as the greatest common factor (GCF) or highest common factor (HCF). It is named after the Greek mathematician Euclid.

The GCD of two numbers is the largest number that divides both of them without leaving a remainder.
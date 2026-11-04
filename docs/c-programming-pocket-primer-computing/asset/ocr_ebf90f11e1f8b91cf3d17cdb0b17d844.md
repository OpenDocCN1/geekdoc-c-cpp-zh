```
```text
reducing 10 and  4
reducing  6 and  4
switching 2 and  4
GCD of  24 and 10 = 2
```
```

# # CALCULATING THE LCM OF TWO NUMBERS VIA RECURSION

The LCM (lowest common multiple) of two positive integers is the smallest integer that is a multiple of those two integers. Some values are shown here:

```
```text
lcm(6,2)   = 2
lcm(10,4)  = 20
lcm(24,16) = 48
```
```

In general, if x and y are two positive integers, you can calculate their LCM as follows:

```
```text
lcm(x,y) = x/gcd(x,y)*y/gcd(x,y)
```
```

Listing 4.17 uses the `gcd()` function that is defined in the previous section in order to calculate the LCM of two positive integers.

# ### LISTING 4.17: LCM.c

```
```c
#include <stdio.h>

int gcd(int num1, int num2)
{
    if(num1 % num2 == 0)
    {
        return num2;
    }
    else if(num1 < num2)
    {
        //printf("switching %d and %d\n", num1, num2);
        return gcd(num2, num1);
```
```
is precisely the implementation of the definition of Fibonacci numbers. The output from Listing 4.12 is here:

```
```
Fibonacci value of 10 = 89
```
```

# CALCULATING THE POWER OF A NUMBER VIA RECURSION

Listing 4.13 displays the contents of `ComputePower.c` that uses recursion to calculate a number raised to a given power.

# LISTING 4.13: ComputePower.c

```
```c
#include <stdio.h>

long computePower(int b,int e, int r)
{
    if( e == 0 ) return r;
    computePower(b, e-1, r*b);
}

int main()
{
    int base = 4, exp = 5;
    long int result;

    result = computePower(base, exp, 1);
    printf("%d to the power of %d = %ld\n",base, exp,
           result);

    return 0;
}
```
```

Listing 4.13 defines the function `computePower()` with the parameters `b`, `e`, and `r`, that correspond to the base, exponent, and result, respectively. This function uses
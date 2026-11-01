Now, addition could proceed correctly by summing the columns in the usual manner and this would yield the same answer if you envision the fixed decimal point two positions to the left of the last digit. By assuming the presence of a decimal point at a fixed location in each number, it is possible to perform arithmetic that is similar to floating point. The same principle involved with fixed point calculations on calculators can be extended to packed decimal calculations as we show next.

Figure 94 gives a program which is an example of using fixed point packed decimals to calculate PI. It is based on the Gregory-Leibniz method which can be summarized as the series: PI/4 = 1 - 1/3 + 1/5 - 1/7 + 1/9 ...

the right hand side of which, in decimal, is:

1 - 0.3333 + 0.2000 - 0.1428 + 0.1111 ...

```
```c
#include <stdio.h>

int main() {
    int i,j=3;
    double pi = 1.0;
    for (i=0;i<500000; i++) {
        if (i%2==0) pi+=1.0/j;
        else pi-=1.0/j;
        j+=2;
    }
    printf("iterations=%d pi=%f\n",i,4*pi);
    return 0;
}
```
```

# Figure 94 Calculation of PI in C

A C program to accomplish this is shown in Figure 94. The final value of i is multiplied by 4 to give PI. The formula converges very slowly so many iterations are needed to obtain even a modest number of digits of accuracy.

When using floating point (double in C), the PI program is simple because the divisions on lines 9 and 10 result in numbers with fractional parts. Thus, the calculation of 1.0/3.0 yields 0.333333333333333 when converted to decimal and printed.

However, a packed decimal division (DP instruction) of the same values yields 0 with a remainder of 1 which is not exactly what the formula requires. So, the question becomes, how can you get a series of numbers such as: 0.3333, 0.2000, 0.1428, 0.1111 and so forth?

The answer is quite simple. First, initialize PI as a large integer packed decimal number such as 10 000 000 000.
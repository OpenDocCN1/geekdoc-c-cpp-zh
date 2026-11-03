If we will not get our desired result. To avoid this problem we can force the leftmost 8 bits to be zero after the right shift. So now this will be as:

```
x = (x<<8) | ((x>>8) & 0x0FF)
```

```
*P13.16 Program to swap first 8 bits with the last 8 bits in a 16-bit integer*
#include<stdio.h>
main()
{
    int num,i;
    printf("Enter number in hexadecimal : ");
    scanf("%x",&num);
    printf("Before swapping, num = %x\n",num);
    bit_pattern(num);
    num=(num<<8) | ((num>>8)&0x0FF) ;
    printf("After swapping, num = %x\n",num);
    bit_pattern(num);
}
```

# Problem 5

Write a program to swap the values of 2 variables using bitwise XOR.

```
*P13.17 Swapping the values without using a temporary variable through bitwise XOR*
#include<stdio.h>
main()
{
    int x,y;
    printf("Enter values for x and y : ");
    scanf("%d%d",&x,&y);
    printf("x = %d, y = %d\n",x,y);
    x=x^y;
    y=x^y;
    x=x^y;
    printf("x = %d, y = %d\n",x,y);
}
```

# Problem 6

Write a program to print the bit pattern of 2's complement of a number

We know that the 2's complement can be found out by adding 1 to the one's complement. Another way to obtain the 2's complement is that, scan the bit pattern from right to left, and invert all the bits after the first appearance of a bit with value 1. For example-

Bit pattern : 0000 0001 0110 0000
2's complement : 1111 1110 1010 0000

```
*P13.18 Program to print the two's complement of a number.*
#include<stdio.h>
main()
```
The & operator can be used to check whether a number is a power of 2 or not. This can be achieved by using the while loop and the arithmetic operator % as follows.

# EXAMPLE

```
1. #include <stdio.h>
int main()
{
    int n, r;
    printf("\n ENTER THE NUMBER :");
    scanf("%d", &n);
    while(n>1)
    {
        r=n%2;
        if(r==0)
            n=n/2;
        else
            break;
    }
    if(n!=1)
        printf("\n The number is not power of 2 ");
    else
        printf("\n The number is power of 2 ");
    return 0;
}
```

r is assigned the value obtained as remainder from this expression.

Using bitwise AND, the program in Example 1 can be rewritten without using the loop or the arithmetic operators.

```
#include <stdio.h>
int main()
{
    int n;
    printf("\n ENTER THE NUMBER :");
    scanf("%d", &n);
    if((n & (n-1))==0)
        printf("\n The number is power of 2 ");
    else
        printf("\n The number is not power of 2 ");
    return 0;
}
```

Bitwise operation

For illustration, let n = 8, n & (n − 1) evaluates to 0000. Here n is represented as four binary digits. Hence

| n & (n − 1) | 1 | 0 | 0 | 0 |
|---|---:|---:|---:|---:|
| n | 1 | 0 | 0 | 0 |
| n − 1 | 0 | 1 | 1 | 1 |
| n & (n − 1) | 0 | 0 | 0 | 0 |

So, the number 8 is a power of 2. But, when n = 12, then

|  | 1 | 1 | 0 | 0 |
|---|---:|---:|---:|---:|
| n | 1 | 1 | 0 | 0 |
| n − 1 | 1 | 0 | 1 | 1 |
| n & (n − 1) | 1 | 0 | 0 | 0 |

Thus, n & (n−1) is not equal to 0. Therefore, it is not a power of 2, though n is divisible by 2.

Masking is a process by which a given bit pattern is converted into another bit pattern by means of a logical bitwise operator. One of the operands in the bitwise operation is the original bit pattern that is to be transformed. The other operand, called mask, is the selected bit pattern that yields the desired conversion. The bitwise AND operator, &, is often used to mask off some set of bits. The following segment of code uses a mask with the value 1 and prints an alternating sequence of 0’s and 1’s.

```
int i, mask=1;
for(i=0; i<16; ++i)
    printf("%d", i & mask);
```

A mask value can be used to check if certain bits have been set. For example, to check whether bits 1 and 3 were set, the number should be masked with 10 and the result tested against the mask.

# EXAMPLE

```
2. #include <stdio.h>
int main()
{
    int n, mask = 10;
    printf("Enter a number: ");
    scanf("%d", &n);
    if((n & mask) == mask)
        printf("Bits 1 and 3 are set");
    else
        printf("Bits 1 and 3 are not set");
    return 0;
}
```

The above example is better understood with the following illustration:

| Variable | Contents | Remarks |
|---|---|---|
| n | any decimal number; binary (16 bits) | x = 0 or 1; byte (most significant); byte (least significant) |
| mask | 10; 0000 0000 0000 1010 |  |
| n & mask | 0000 0000 0000 0000 / 0000 0000 0000 1010 / 0000 0000 0000 1000 | byte (most significant); byte (least significant); Bit number |


In case the value of n & mask is equal to mask, that is, if the bits 1 and 3 marked as x are equal to 1, then the bits in 1 and 3 positions are set to 1. Another important example of mask is 255; its binary equivalent is 0000 0000 1111 1111. As only the lower order
```
/*P13.11 Program to test any bit in an integer*/
#include<stdio.h>
main()
{
    int a,bit,mask,bitposition;
    printf("Enter an integer : ");
    scanf("%d",&a);
    printf("Enter the bit position : ");
    scanf("%d",&bitposition);
    mask=1<<bitposition;
    printf("a = %d\t",a);    bit_pattern(a);
    if((a&mask)==0)
        bit=0;
    else
        bit=1;
    printf("The bit at position %d is %d\n",bitposition,bit);
}
```

If we want to manipulate all bits one by one, then we can use a loop, for example this program will switch on all the bits in the integer variable a.

```
/*P13.12 Program to switch on all the bits in an integer variable*/
#include<stdio.h>
main()
{
    int a,mask,i;
    printf("Enter the value of a : ");
    scanf("%d",&a);
    printf("%d\t",a);  bit_pattern(a);
    for(i=0;i<=15;i++)
    {
        mask=1<<i;
        a=a|mask;  /*switch on the ith bit*/
    }
    printf("%d\t",a);  bit_pattern(a);
}
```

There is one other way also to calculate the appropriate mask for a particular bit position. We can take an array of masks as-

unsigned int arr_mask[] = { 0x1, 0x2, 0x4, 0x8, 0x10, 0x20, 0x40, 0x80, 0x100, 0x200, 0x400, 0x800, 0x1000, 0x2000, 0x4000, 0x4000};

Now the mask for manipulating any bit can be calculated as-
    mask = arr_mask[bitposition];

For example to switch on the 4th bit we can write
    x = x | arr_mask[4];

# 13.9 Some additional Problems

# Problem 1

Write a program to print bit pattern of a 16 bit integer.
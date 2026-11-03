Decrypted data : 0000 1111 0101 0011 ( By applying ~ to encrypted data )

# 13.5 Bitwise Left Shift ( << )

This operator is used for shifting the bits left. It requires two operands. The left operand is the operand whose bits are shifted and the right operand indicates the number of bits to be shifted. On shifting the bits left, an equal number of bit positions on the right are vacated. These positions are filled in with 0 bits. Let us take an integer variable a = 0x1346. The binary representation of x is- 0001 0011 0100 0110 Now we'll find out a << 4

Initial Bit pattern

0001 0011 0100 0110

Bit pattern after left shifting

0001 0011 0100 0110 0000
Lost Bits
Bits filled

On shifting all bits to the left by 4, the leftmost 4 bits are lost while the rightmost 4 bit positions become empty which are filled with 0 bits.

```
/*P13.5*/
#include<stdio.h>
main()
{
 int a;
 printf("Enter value for a : ");
 scanf("%d",&a);
 printf("a = %d\t",a);   bit_pattern(a);
 a=a<<2;
 printf("a = %d\t",a);   bit_pattern(a);
}
```

# 13.6 Bitwise Right Shift ( >> )

This operator is similar to the left shift operator, except that it shifts the bits to the right side. On shifting the bits right, an equal number of bit positions on the left are vacated. These positions are filled in with 0 bits in unsigned integers. We'll again take a variable a = 0x1346, and this time we'll find out a >>

Initial Bit pattern

0001 0011 0100 0110

Bit pattern after right shifting

0000 0001 0011 0100
Bits filled
0110
Lost Bits

Right shift in an unsigned integer

In right shift if the first operand is a signed integer, then the result is compiler dependent. Some compilers follow logical shift while others may follow arithmetic shift.
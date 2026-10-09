
## Significant Bits

When working with a group of bits as a bit pattern we still tend to refer to the most significant and least significant bits, even though these terms really only apply when you are interpreting the bit pattern as a number. The most significant bit is associated with the largest power of two in a place value system and the least significant with the smallest power. Conventionally we write the most significant bit on the far left, following the way we write place value numbers in decimal:

![](img/5f2ea21c2077d473344a0fdf144677b9_72_0.png)

You can assign all of the bits in a bit pattern a number starting from the lowest-order bit. Can you use the bit position as an address? Yes, as it is trivial to generate a mask from a bit position p:

```
mask = 1 << p
```

and if you want a mask corresponding to more than one position you can use:

```
mask = 1 << p1 | 1 << p2 | 1 << p3 ...
```

This isn't a common requirement, but it can be useful when creating code that works with hardware registers that are often defined in terms of bit position.

## Endianism

A problem that often arises in bit manipulation is endianism and it is closely connected to the ideas of bit position and byte addressing. When you design a computer there is a choice to be made. If parts of a word, say each byte, has a separate address do you store the low-order bits at low addresses, little-endian, or at high addresses, big-endian?

![](img/5f2ea21c2077d473344a0fdf144677b9_72_1.png)

Although this is expressed as a problem that has to do with integers, it applies to any bit pattern that is broken up into bytes – what order do you reassemble it in. It also applies to bytes that are sent over any communication link – should the most significant byte be sent first or last?

Often you can ignore endianism as the machine takes care of it for you. If you save a 16-bit int then it will be saved in the order the machine uses and when you retrieve it the same order will be obeyed. Generally endianism only matters when the bytes have been acquired one-by-one from an external source such as hardware, a file or a communications link. Within a program, endianism only matters when you are aliasing a pointer or using a union, see Dive 15.

For example, consider a 2-byte int and alias it to a 2-byte array.

```
union endian{
    unsigned short myint;
    unsigned char mychar[2];
};
test.myint=0x00FF;
printf("%x\n",test.mychar[0]);
printf("%x\n",test.mychar[1]);
```

The union aliases myint and mychar. We then set myint so that all eight of its low-order bits are 1. If the machine is little-endian, as in the case of x86 and ARM, then the low-order bits are stored in mychar[0]. If the machine is big-endian, e.g. Atmel AVR32, the low-order bits are stored in mychar[1].

For example, creating a union to access the separate color channels ARGB – Alpha, Red, Green and Blue values in an unsigned 32-bit int is an example of something that changes according to endianism. As A is the high-order byte and B the low-order you might expect the union to be:

```
union Pixel{
    struct {unsigned char a,r,g,b};
    uint32_t value;
};
```

and this works for big-endian systems as b the least significant byte has the highest address in the union.

However the x86 and ARM are little-endian. So the ARGB bytes are stored in the opposite order with a at the lowest address in the union:

```
union Pixel{
    struct {unsigned char b,g,r,a};
    uint32_t value;
};
```

This is also a problem when data is transmitted in big-endian format over most Internet protocols – IPv4, IPv6, UDP, TCP etc. What this means is that if you are using a machine with little-endian format you transmit mychar[1] before mychar[0] to send a 16-bit integer when using almost any Internet protocol. That is, it is the order that data is sent and received rather than addressing that is variable.

Notice that some machines support both big- and little-endian and you can select which is used. It is also possible for different data formats, e.g. integer and floating point, to use different orders. You will also find issues of which byte goes first when you use memory-mapped devices. In this case, a careful reading of the data sheet usually solves the problem. If you are getting strange results and are sending data processed in bytes then you need to consider endianness.

## Rotate

There is another form of shift – the left or right rotate – and while most processors have an instruction that will perform this type of shift in a single operation, for reasons of history C doesn’t have a rotate operator.

A right rotate shifts all of the bits to the right and uses the least significant bit that is shifted out as the new most significant bit. That is, the low-order bit is shifted into the high-order bit. You can see that this is rotation of the bits.

Similarly a left rotate shifts all of the bits left and moves the high-order bit to become the new low-order bit. Again, you can see that this rotates the bits in the other direction. Rotations don’t correspond to simple multiplication or division and they aren’t useful in the same way as left and right shifts are in isolating bits. What they are used for is in cryptography and signal processing.

C may not have a rotate operator, but it is easy to implement a rotate using left and right shifts and logical operators. For example, a right rotate is:

```c
unsigned int data=0xF;
data= data>>1 | data<<31;
```

The idea is easy enough to understand. First we perform a right logical shift which leaves the most significant bit zeroed. Next we perform a left logical shift 31 times to move the lowest significant bit to become the highest significant bit. The two are ORed together to give the result 0x80000007.

You can see the general principle. If you want a right rotate of n bits of a 32-bit int then use:

```c
data = data>>n | data<<32-n;
```

Similarly, if you want a left rotate of n bits of a 32-bit value then use:

```c
data = data<<n | data>>32-n;
```

Notice that n cannot be negative or equal to 32, which would trigger undefined behavior. Also notice that data has to be unsigned so as to use logical shifts.

It is said that most compilers will detect the above idioms and convert the instructions into a machine code rotate instruction if possible. GCC does this optimization, but only if you make sure that the rotation is positive. That is:

```c
unsigned int data=0x0F;
data= data>> (unsigned) 1 | data<< (unsigned)31;
```

compiles to:

```
ror eax
```

where ror is a rotate right instruction. If you leave off the unsigned qualifiers the line compiles to the equivalent right shift and left shift ORed together. It would be better if C had a rotate operator.

## Bit Fields

There is an alternative to some bit manipulation – the bit field. A bit field is a way of breaking down the storage into even smaller units than bytes. You can define a bit field within a struct by following the field definition by a colon and the number of bits. For example:

```c
struct Bits{
int bit1:1;
int bit2:1;
};
```

creates an int, say four bytes, but only the first two bits are used. This is somewhat like a union, but in this case the bit fields share the int. For example:

```c
struct Bits bits;
bits.bit1=1;
bits.bit2=1;
printf("%d\n",bits);
```

If we make a small change to the struct then you can see that you can work with more than just single bits:

```c
struct Bits{
int byte:8;
int bit1:1;
int bit2:1;
}bits;
```

This divides up the int so that the first eight bits are called byte, followed by two single-bit fields. Now we can write:

```c
bits.bit1=1;
bits.bit2=1;
bits.byte=255;
printf("%d\n",bits);
printf("%d\n",bits.byte);
```

you will discover that bits is 1023 and bits.byte is -1.

As the int being shared is a signed int then so are all of the fields including the single-bit fields:

```c
printf("%d\n",bits.bit1);
```

prints -1.

The standards are unclear on whether a bit field int is to be interpreted as signed or unsigned.

You can change the interpretation of a single field using:

```c
struct Bits{ 
unsigned int byte:8;
int bit1:1;
int bit2:1;
}bits;
```

bits.byte now prints 255, but bits.bit1 still prints -1.

You can often use other types, not just int, but this goes beyond standard C. If you mix types then usually the largest type is used. For example:

```c
struct Bits{ 
unsigned char byte:8;
char bit1:1;
char bit2:1;
}bits;
```

usually allocates a char for the first eight bits and another char for the next two bits, giving an overall size of two bytes for the struct. It is usually better to keep all of the bit fields the same type within a struct.

In general no padding is used in a bit field, but if you allocate more bits than an int can represent, a second int is used. If you want to force a new allocation so that a bit field is aligned to an address boundary you can include an unnamed bit field of size zero. For example:

```c
struct Bits{ 
unsigned int byte:8;
int :0;
int bit1:1;
int bit2:1;
}bits;
```

allocates two ints with bits.byte occupying the first eight bits of the first int and bits.bit1 and bits.bit2 at the start of the second byte.

You can form expressions with bit fields and any result will not overflow into an adjacent bit field i.e. the bit fields are isolated. For example:

```c
bits.byte = 255;
bits.byte++;
```

results in bits.byte overflowing and being set to zero, but bits.bit1 isn't changed.

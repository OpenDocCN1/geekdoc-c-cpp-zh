For a 16-bit value we have:

```
```
int16_t num = 42;
int bit = 0;
for (int i = 0; i <= 16; i++)
{
bit = num / (1 << (16 - i));
printf("%d", bit);
num = num % (1 << (16 - i));
}
```
```

This divides the number by a decreasing power of two to find out if it needs a 1 or a 0 and then reduces the number to the remainder. Recall that a left shift is the same as multiplying by two.

Of course, we don't need to convert decimal numbers to binary in this explicit way as the command:

```
```int16_t num = 42;```
```

does it for us without us even giving it a thought. The compiler doesn't store decimal 42 in the variable; instead it converts the decimal value into binary and stores it in num.

So we already have the binary representation of 42 stored in num and working out what the bits would be is crazy as we already have the bits stored in num! All we have to do to see the binary representation is to print the bits of num out one by one and in the right order. This is easy using a right shift and a one-bit mask – see Dive 5, Bits and More Bits:

```
```
int16_t num = 42;
int bit=0;
for (int i = 0; i <= 16; i++)
{
bit = (num >> (16-i)) & 0x01;
printf("%d", bit);
}
```
```

If you are happy with hex you don't even need to split out the bits one at a time:

```
```
int16_t num = 42;
printf("%X\n",num);
```
```

Which displays 2A, the hex for 00101010. The beauty of hex is that you can convert it to binary and vice versa one symbol at a time. For example, 2 is 0010 and A is 1010 which gives the complete binary value 0010 1010. Going the other way you can convert any binary value to hex working four bits at a time. That is 0010 1010 is 2 A – hardly any math needed.

That is, when you store 42 in a variable it is converted to binary without you doing anything at all. Variables do not store decimal values, but the bit patterns that represent the decimal values using binary.
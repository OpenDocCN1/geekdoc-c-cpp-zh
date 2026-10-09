As the int being shared is a signed int then so are all of the fields including the single-bit fields:

```
printf("%d\n",bits.bit1);
```

prints -1.

The standards are unclear on whether a bit field int is to be interpreted as signed or unsigned.

You can change the interpretation of a single field using:

```
struct Bits{ 
unsigned int byte:8;
int bit1:1;
int bit2:1;
}bits;
```

bits.byte now prints 255, but bits.bit1 still prints -1.

You can often use other types, not just int, but this goes beyond standard C. If you mix types then usually the largest type is used. For example:

```
struct Bits{ 
unsigned char byte:8;
char bit1:1;
char bit2:1;
}bits;
```

usually allocates a char for the first eight bits and another char for the next two bits, giving an overall size of two bytes for the struct. It is usually better to keep all of the bit fields the same type within a struct.

In general no padding is used in a bit field, but if you allocate more bits than an int can represent, a second int is used. If you want to force a new allocation so that a bit field is aligned to an address boundary you can include an unnamed bit field of size zero. For example:

```
struct Bits{ 
unsigned int byte:8;
int :0;
int bit1:1;
int bit2:1;
}bits;
```

allocates two ints with bits.byte occupying the first eight bits of the first int and bits.bit1 and bits.bit2 at the start of the second byte.

You can form expressions with bit fields and any result will not overflow into an adjacent bit field i.e. the bit fields are isolated. For example:

```
bits.byte = 255;
bits.byte++;
```

results in bits.byte overflowing and being set to zero, but bits.bit1 isn't changed.
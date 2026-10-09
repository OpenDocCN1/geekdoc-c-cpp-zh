
Similarly if you use:
`value & ~mask;`

then the bits specified in the mask are set to zero

sets result to 0xFFFC, i.e. it unsets the first two bits.

As well as setting and unsetting particular bits, you might also want to “flip” the specified bits, i.e. negate them so that if the bit was a one it is changed to a zero and vice versa. You can do this using the XOR, exclusive or, operator:
`value ^ mask`

which flips the bits specified by the mask. For example:
`int mask = 0x03;`
`int value = 0xFFFF;`
`int result = value ^ mask;`
`printf("%X\n",result);`

sets result to 0xFFFC because it changes the lower two bits from ones to zeros. Again, bits not specified by mask are unaffected.

If you want to update the flag rather than derive a new result, you can use:
`&=`
`|=`
and:
`^=`

to perform the update directly. For example:
`int value = 0xFFFF;`
`int value ^= 0x03 ;`
`printf("%X\n",value);`

To summarize:

- Create a mask that has 1 at the position of each bit you want to change.
- To set the designated bits OR the mask with the value.
- To unset the designated bits AND the NOT of the mask with the value.
- To flip the designated bits XOR the mask with the value.

Bits in the mask that are 0 are unaffected by any of the operations.

## A Single Function To Write Bits

Let's combine these operations into a single bitWrite operation that uses a mask to specify the bits to change and a data value to specify what each bit should be set to. If you regard the mask as the addresses of the bits to be changed then this writes the data to those bits and only those bits.

For example:

```
int mask = 0x03; //011
```

specifies that the first two bits should be modified and:

```
int data = 0x02; //010
```

specifies that the first bit should be set to zero and the second should be set to one.

The trick to working out how to do this is to construct one mask to set the bits that need to be set and another to unset the bits that need to be unset.

Then if a bit is to be set, it needs a 1 in the mask and a 1 in the data and the mask to set bits is:

```
setmask = mask & data
```

If a bit is to be unset it needs a 1 in the mask and 0 in the data, so the mask to reset bits is:

```
resetmask = mask & ~data
```

Applying both to the value gives the required result:

```
(value | setmask) & ~(resetmask) =
(value | (mask & data)) & ~(mask & ~ data)
which, after simplification, is:
value & ~mask | mask & data
```

Using this it is easy to create a function to do the job:

```
int bitWrite(int value, int mask, int data)
{
  value = value & ~mask | mask & data;
  return value;
}
```

For example:

```
printf("%b\n", bitWrite(0xFF, 0x0F, 0x05));
```

The mask means that only the first four bits are modified and the data sets them to 0101 which is the result of 11110101.

You can use bitWrite to set any group of bits to any value.

## Reading Bits

So far we have focused on writing bits, but we also often want to read a bit pattern and the method is more or less the same and relies on masks. As before, if you create a mask with bits set corresponding to the bits you want to read, then:

```
value & mask
```

returns `0` if and only if all of the bits the `mask` specifies are `0`.

Similarly:

```
~ value & mask
```

returns `0` if and only if all of the bits the `mask` specifies are `1`.

Usually, you only want to test for a single bit. For example:

```
int value = 0x1F;
int mask = 0x10;
int result = ~value & mask;
```

tests the fifth bit in `value` which is `1` and so `result` is `0`.

If you test for the fifth bit to be a zero using:

```
int value = 0x1F;
int mask = 0x10;
int result = value & mask;
```

then the result is non-zero, `16` to be precise.

If you want to convert the test results to Boolean values you can use the logical operator `!`. For example:

```
!(~value & mask)
```

is `true` if and only if all of the bits in `value` specified by `mask` are `1` and `false` otherwise.

Similarly:

```
!(value & mask)
```

is `true` if and only if all of the bits in the `value` specified by `mask` are `0` and `false` otherwise.

If you want to just read the bits specified by the mask, simply `AND` it with the value:

```
value & mask
```

For example, to read the bottom four bits you can use:

```
result = value & 0x0F;
```

## Shifting Values

A very common requirement when reading bits is to move them to a suitable location within the group of bits. To do this you need the shift operators. The `<<` operator shifts the pattern of bits to the left, shifting zero into the low-order bit. So, for example:

```
int data = 0x0F;
int result = data << 4;
```

shifts the bit pattern in data four places to the left and so result contains 0xF0.

Don't try specifying a negative shift as this is undefined behavior.

Similarly the `>>` operator shifts to the right, but there is a small complication concerning what is shifted into the new bit positions. What happens depends on whether the value being shifted is signed or unsigned. For an unsigned value 0 is shifted into the highest-order bit. For a signed value the same bit is shifted in as the one moved. That is, if the highest-order bit was a 1 then a 1 is shifted into the vacant position and it if was a 0, a 0 is shifted in.

You can see that in the signed case the motivation with a right shift is to maintain the sign. That is, a shift keeps a positive number positive and a negative number negative. This sort of shift is usually called an arithmetic shift as distinct from a logical shift that always shifts a 0 in. You can always force a logical shift by casting the value to an unsigned type.

Notice that a left shift always shifts a 0 in, but this can change the sign of the value as a new bit becomes the sign bit. For example:

```
int data = 0x0F;
int result = data >>3;
```

shifts the bit pattern in data three places to the right and so result contains 1 since 1111 shifted three places right is 0001.

For integers shifting one place to the left is the same as multiplying the value by two and shifting one place to the right is the same as integer division by two, but only for positive values. For example:

```
int data = 1;
int result = data <<1;
```

stores 2 in result and:

```
int data = 8;
int result = data >>1;
```

stores 4 in result.

Things are slightly more complicated for negative values. If you try:

```
int data = 7;
int result = data >>1;
```

then `result` is 3 which is what you would get with integer division, i.e. 3.5 is truncated or rounded down to 3. However, if you try:

```
int data = -7;
int result = data >>1;
```

you will find that `result` is -4. This is not what you would get with integer division, which would give -3 after truncation. Right shift divides by two, but with rounding towards the next smallest negative integer. This is a subtle point that often causes errors.

The reason for this behavior is the way the sign bit is extended. For example:

```
int data = -1;
int result = data >>1;
```

stores -1 in `result`. The reason is that the initial bit pattern is all ones, i.e. 32 bits all set to one, and so shifting one place to the right shifts in another 1 as the high bit. That is, -1 is the same as 0xFFFFFFFF and the sign bit is 1 so a shift right moves a one into the high-order bit, giving -1 again.

Compare this to:

```
unsigned int data = -1;
int result = data >>1;
```

In this case a zero is shifted into the high bit and the value stored in `result` gives zero followed by 31 ones, which is a positive value equal to 2147483647. Notice that the -1 is stored in `data` as 0xFFFFFFFF, but this is interpreted as a positive value when stored in an `unsigned int`. The result of the shift is 0x7FFFFFFF, which is a positive number when assigned to a signed `int`. What this means is that you can use either right and left shifts or multiplication and division by two to do almost the same job with a little care over negative values. Shifts are much faster than multiplication and division because the hardware generally supports a direct shift operation in a register.

If you want a logical right shift on a signed value then the simplest way of implementing it is to use a cast:

```
int data = -1;
int result = (unsigned int) data >>1;
```

You can also use `<<=` and `>>=` to shift the value of a variable in place. For example:

```
int data = -1;
data <<= 1;
```

shifts the bit pattern in `data` one place to the left and stores the result in `data`, i.e. it shifts `data` one place to the left.

For example:
```
signed int value = -5;
```
if the machine uses two's-complement representation then the bit pattern is:
```
11111111111111111111111111111011
```
and:
```
value | 0x4
```
changes the third bit to 1, i.e. -1 in two's-complement.

As long as you assume a specific representation for the signed value then the logical operation is usually well defined as the bitwise application of the operator on the bit pattern. It is the representation that is implementation-dependent and not the operation.

# ## Masks

Bitwise operations are the key to accessing individual bits. We usually think of this as setting or unsetting a particular bit or testing its state. You can set and unset bits using another value, usually called a mask, that defines the bits to be changed. In this sense the bits in the mask act as the addresses of the bits that you want to work with. For example, if you only want to change the first (least significant) bit then the mask would be `0x01`. If you wanted to change the first and second bits the mask would be `0x03` and so on. That is, the mask has the bits you want to access set to one with all other bits zero.

The mask gives the address of the bits you want to work with and what you do to those bits depends on the operation you use to combine the mask with the value. For example:
```
value | mask;
```
returns a bit pattern with the same bits set to one as in the mask. Notice that the bits that the mask doesn't specify, i.e. are zero in the mask, are left at their original values.

If you OR the mask you set the addressed bits to one and leave all of the others unchanged. For example:
```
int mask = 0x03;
int value = 0xFFF0;
int result = value | mask;
printf("%X\n",result);
```
sets result to `0xFFF3`, i.e. it sets the first (least significant) two bits.
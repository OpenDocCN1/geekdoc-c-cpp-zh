After discovering the truncation limits on numbers, the next obvious step is to test whether these 32-bit numbers are also limited by being signed numbers rather than unsigned numbers.

```
.equ NUM1 = 0xFFFFFFFF
.equ NUM2 = 0x00000001

.if (NUM1 < NUM2)
.warning "NUM1 is less than NUM2."
.endif

.if (0xFFFFFFFF < 0x00000001)
.warning "0xFFFFFFFF is less than 0x00000001."
.endif
```

In the above code, NUM1 has a value of 0xFFFFFFFF which is 4,294,967,295 or 2^32 – 1 if the number is treated as an unsigned 32-bit integer. If instead NUM1 is treated as a signed 32-bit integer, then the value 0xFFFFFFFF assigned to it gives it a value of –1 in 2’s compliment format. When the above code is inserted into the source code of a Microchip Studio AVR assembly language project, and the project is built, the first comparison evaluates to true, and the warning message appears at the bottom of Microchip Studio. Note that this comparison uses the less-than operator (<) to determine if NUM1 is less than NUM2. NUM1 can only be less than NUM2 if NUM1 is 0 or a negative number. This proves that the the equated numbers are treated as signed 32-bit integers, rather than unsigned 32-bit integers. In the second comparison in the above code, the same values that were assigned to NUM1 and NUM2 are directly compared. This comparison results in false, which means that the warning message does not appear at the bottom of the Microchip Studio window for the second comparison.

A final test for signed numbers is shown in the following code.

```
.equ NUM1 = 0x7FFFFFFF
.equ NUM2 = 0x00000001

.if (NUM1 < NUM2)
.warning "NUM1 is less than NUM2"
.endif
```

In the above code, NUM1 is assigned a value of 0x7FFFFFFF, which is the maximum positive value that a signed 32-bit number can have. In this number, all bits are set, except for the most significant bit, which is used as the sign bit. Because of this, the number is effectively a 31-bit number because the most significant bit is not used. The maximum
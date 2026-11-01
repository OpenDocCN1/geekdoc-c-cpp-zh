![](bbox=[0.056, 0.042, 0.923, 0.228])

# Figure 14 SS Formats

As can be seen, in one format, the length byte is taken as an unsigned 8 bit number. In the other variation, the length byte is interpreted as two unsigned 4 bit numbers.

The instruction::

```
MVC 100(8,R13),200(R13)
```

Where the opcode of a MVC is D2₁₆ would, in machine language, look like:

```
D207D064D0C8
```

You can see the opcode is D2, the length is 07, the first base is D₁₆, the first displacement is 064₁₆, the second base is D₁₆ and the second displacement is 0C8₁₆.

Notice that the length is not 8. When represented in machine language, the length is always one less. Thus 0 means 1, 1 means 2 and so forth.

As noted, some SS instructions divide the length byte into two 4 bit fields in order to get 2 lengths. This is mainly used with the class of arithmetic instructions known as decimal or packed. For example, the SS instruction Add Decimal (or Add Packed) with the mnemonic AP has two lengths. The length subfields give the length of the first and second operands, respectively. So, a typical AP instruction might look like:

```
AP VAL1(5),VAL2(3)
```

This means to add the three byte field from the second operand (VAL2) to the contents of the 5 byte field specified as the first operand (VAL1) and leave the result in the first operand. Translated to explicit format the above might look like:

```
AP 32(5,R13),64(3,R13)
```

which would, given the opcode of FA₁₆ yield the machine instruction:
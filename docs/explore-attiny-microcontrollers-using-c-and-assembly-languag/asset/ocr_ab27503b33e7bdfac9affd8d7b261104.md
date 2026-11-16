This means that the program counter is incremented by one after the instruction has executed. The state of the status register is unchanged after the LDI instruction. This is shown in the manual as dashes under each bit of the status register. Section or Chapter 1 of the manual gives the meanings of the values of various flags.

An example of usage of the LDI instruction follows the status register in the manual and can be seen in Figure 6.12. This is followed by the size of the instruction which is one 16-bit word, or two bytes. Finally the manual shows that the LDI instruction takes one clock cycle to execute (not included in Figure 6.12). Figure 6.15 shows the encoding of the final two instructions of the example program, the ADD and RJMP instructions.

```
r : Source register address
d : Destination register address

| 0000 | 11rd | dddd | rrrr |
| 0000 | 1111 | 0000 | 0001 | add r16, r17

1 0001 = 17 (R17)
1 0000 = 16 (R16)
```

```
k : Constant address

| 1100 | kkkk | kkkk | kkkk |
| 1100 | 1111 | 1111 | 1100 | rjmp loop

1111 1111 1100 = 4
```

Figure 6.15: Encoding of the ADD and RJMP Instructions

The ADD (Add without Carry) instruction always starts with 00001, followed by the MSB of the source register address, then the MSB of the destination register address. Four bits of the destination register follow and then four bits of the source register. As shown at the top of Figure 6.15, each 5-bit register address is made up of an initial bit and then the four bits that follow. In the example in the figure, the source address is 17 (0b10001) which addresses R17 and the destination address is 16 (0b10000) which addresses R16. A five bit address is capable of addressing 2^2 = 32 address locations from 0 to 31 which correspond to registers R0 to R31 from the register file. Refer to the ADD instruction in the instruction set manual to see which status register flags are changed after the ADD instruction is executed.
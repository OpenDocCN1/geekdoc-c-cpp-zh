The LPM (Load Program Memory) instruction is used to get a byte from the program memory address that the Z register currently contains. The Z register is effectively pointing to this address location, and can be referred to as a pointer register. There are two options when using the Z register with LPM. One is to simply do the following.

```
lpm r16, Z
```

This fetches the byte that the Z register is pointing to in program memory and puts the byte into R16. The other option is the following, as used in our example program.

```
lpm r16, Z+
```

When Z is followed by +, this means, “get the byte that Z is pointing to and then increment Z by 1”, which means that after the instruction has executed, Z will point to the next byte, following the byte just read. Using LPM in this way lets us access each DB byte in order, starting from the first byte, without the need for a separate increment instruction to increment the Z register. SUBI (Subtract Immediate) is used to subtract 0 from R16 after the LPM instruction. This is done to force the status register and the zero flag in the status register to update. We are looking for the null terminator at the end of the string of data, in order to determine when we have reached the end of the data defined by DB. When this null terminator, or value of zero, does get loaded into R16, the status register does not change. Even though R16 contains zero, the Z flag in the status register does not change because this flag only changes after an arithmetic or logic operation. By subtracting 0 from R16, an arithmetic operation is performed, causing the status register to update. Subtracting 0 from R16 updates the status register, but does not alter the data in R16. After SUBI has executed, the Z flag from the status register is checked using the BRBC instruction to see whether we have reached the end of the constant data string. BRBC (Branch if Bit in SREG is Cleared) is used to jump back to the LPM instruction and get the next constant data byte from program memory if the zero flag of the status register is not clear, when R16 does not contain 0. When R16 does contain zero, BRBC will not branch, but execute the code below it, which is an infinite loop.

# Running the Example Code

If you have not done so already, enter the DB example code from the previous listing into the main.asm file from the test_asm project, as we have been doing to test various code
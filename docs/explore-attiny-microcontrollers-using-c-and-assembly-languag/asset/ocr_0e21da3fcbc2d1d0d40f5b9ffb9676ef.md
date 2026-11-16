# CBR (Clear Bits in Register)

CBR clears bits in a register by performing a logical AND between the register and the compliment of immediate data. This means that all bits in the immediate data that are set, result in the same bits in the destination register being cleared, as the first two lines of the following code show.

```
ldi    R16, 0xA5
cbr    R16, 0xF0    ; Mask is 0x0F

ldi    R16, 0xA5
andi   R16, 0xF0    ; Compliment the mask value: 0xF0
```

In the first line of code above, 0xA5 is loaded to R16. In the second line of code, CBR is used on R16 with a mask value of 0x0F. This is not the equivalent of ANDI R16, 0x0F because the compliment of the mask value is used, meaning that all bits in the mask value of 0x0F are inverted, causing the mask value to become 0xF0 before performing the ANDI. The result is that the value left in R16 after the CBR instruction has executed in the above example is 0xA0.

The second two lines of code above show the equivalent code using ANDI. 0xF0 is used with ANDI, which is the compliment of 0x0F. Both CBR and ANDI in the above code disassemble to ANDI R16,0xF0 which means that the assembler program must be inverting the mask value when it comes across the CBR instruction and then changes CBR to ANDI.

# 11.2.1.6 Register Set, Clear and Test Instructions

# TST (Test for Zero or Minus)

TST tests if a register contains zero or a negative value by performing a logical AND on the register and itself. This causes the status register flags S, V, N and Z to update according to what the register contains. In the code that demonstrates the use of constant data in Flash memory in section 9.3.2.2 of Chapter 9, we used a trick to update the status register Z flag by subtracting 0 from R16 to find out if R16 contained zero. In this code we could have used the TST instruction instead, as follows.

```
check_0:
lpm    r16, Z+    ; Load byte from program memory
tst    r16        ; Loop if result not zero
brbc   SREG_Z, check_0
```

This code was taken from the example code in section 9.3.2.2, near the bottom of the listing. TST causes the Z flag to update, just as subi r16, 0 did in the original code.
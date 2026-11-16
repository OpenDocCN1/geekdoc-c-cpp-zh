# 6.9.2 I/O Direct Addressing

I/O direct addressing moves data between a register and I/O location. Both the register address and I/O register address are encoded in the instruction, making it a direct addressing instruction. Figure 6.18 shows a diagram of I/O Direct addressing from the AVR Instruction Set Manual. An example of I/O direct addressing is the OUT instruction as shown in Figure 6.19.

# 3.3 I/O Direct

![](bbox=[0.321, 0.311, 0.851, 0.521])

Figure 6.18: I/O Direct Addressing from the AVR Manual

| 1011 | 1AAr | rrrr | AAAA |
|---|---|---|---|
| 1011 | 1011 | 0000 | 0110 |

Figure 6.19: Encoding of the OUT Instruction with Example

So far we have only used the OUT instruction in examples that initialize the stack pointer. In the example in Figure 6.19, OUT is used to move the contents of R16 to the PINB register. The PINB register is one of the 64 I/O registers mapped in data memory space and is one of the registers used to control the I/O pins of the AVR. In the line of code shown in Figure 6.19, PINB resolves to the address 0x16 (not to be confused with register R16 used in this example). To see the addresses of I/O registers, refer to the Register
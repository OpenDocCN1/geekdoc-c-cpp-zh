
### 6.9.1 Register Direct Addressing

AVR register direct addressing has two variants, namely single register and two register direct addressing. Figure 6.16 shows two register direct addressing taken from the AVR Instruction Set Manual.

![](img/83ef13a6c66cc7882b2f357e97f451dc_129_0.png)

Take special note that the diagrams of addressing modes in the AVR instruction set manual are simplifications and do not show exact bit positions of the address bits of instructions.

An example of single register direct addressing is the CLR (Clear Register) instruction. The full address of the destination register is encoded in the instruction allowing the instruction to directly address the register. Figure 6.17 shows how the address of a register file register is encoded in the CLR instruction – it is actually encoded twice because the source and destination are the same register.

![](img/83ef13a6c66cc7882b2f357e97f451dc_129_1.png)

### 6.9.2 I/O Direct Addressing

I/O direct addressing moves data between a register and I/O location. Both the register address and I/O register address are encoded in the instruction, making it a direct addressing instruction. Figure 6.18 shows a diagram of I/O Direct addressing from the AVR Instruction Set Manual. An example of I/O direct addressing is the OUT instruction as shown in Figure 6.19.

### 3.3 I/O Direct

![](img/83ef13a6c66cc7882b2f357e97f451dc_130_0.png)

Figure 6.18: I/O Direct Addressing from the AVR Manual

| 1011 | 1AAr | rrrr | AAAA |
|---|---|---|---|
| 1011 | 1011 | 0000 | 0110 |

Figure 6.19: Encoding of the OUT Instruction with Example

So far we have only used the OUT instruction in examples that initialize the stack pointer. In the example in Figure 6.19, OUT is used to move the contents of R16 to the PINB register. The PINB register is one of the 64 I/O registers mapped in data memory space and is one of the registers used to control the I/O pins of the AVR. In the line of code shown in Figure 6.19, PINB resolves to the address 0x16 (not to be confused with register R16 used in this example). To see the addresses of I/O registers, refer to the Register Summary section of the datasheet for the ATtiny part being used. In the *Register Summary* section of the ATtiny25/45/85 datasheet, it can be seen that there are 64 I/O registers from 0x00 at the bottom of the table to 0x3F at the top of the table. Find address 0x16 in the table and note that it has the name PINB shown in the next column of the table.

Again, the values in the instruction are interleaved. Below the instruction encoding blocks in Figure 6.19 are the values for the I/O location address and source register after they have been extracted from the instruction and assembled as consecutive bits. The I/O location address has 6 bits represented by 6 'A' characters. From this we can deduce that it can address 2^6 = 64 locations from 0 to 63, or 0x00 to 0x3F in hexadecimal. In other words it can be used to address the 64 I/O registers mapped in data memory. There are 5 bits in the instruction in the figure that are labeled 'r' that represent the registers from the register file. We now know that 2^5 = 32, therefore 32 registers from the register file can be addressed by this instruction – in other words all of the registers from R0 to R31.

### 6.9.3 Other Addressing Modes

Refer to the *AVR Instruction Set Manual* for other addressing modes. The other addressing modes will be better understood as we look at more instructions throughout the book. Indirect addressing modes do not have the address of the target register or memory location encoded in the instruction, but rather rely on the target address to be loaded to a register or registers before calling the indirect addressing instruction.

### 6.10 Summary

- Clock pulses drive the internal circuitry of a microcontroller and cause it to fetch and execute instructions.
- It is easy to calculate the period of a clock pulse if given the frequency, or calculate the frequency of a clock pulse if given the period.
- The program counter (PC) continually increments, addressing each consecutive instruction in program memory until a jump or branch instruction is executed which loads the PC with a new address.
- Microcontrollers have an address bus for addressing program and data memory, a data bus for moving data between the microcontroller and memory or I/O devices, and a control bus with control lines such as chip select and read and write lines.
- AVR microcontrollers have a Harvard architecture with separate buses for program memory and data memory to enhance performance.
- The basic function of a microcontroller core is to fetch and execute instructions from program memory.
- The status register of a microcontroller contains information on the result of the most recent arithmetic operation.
- A stack is used to store temporary data, preserve register values and store the return address of subroutines and interrupt handlers.
- The stack is set up by loading a RAM address to the stack pointer register.
- Microcontroller machine language instructions are encoded in binary format. Encoding details can be found in the instruction set manual.
- Addressing modes refer to how an instruction addresses registers or memory locations.

This has been a fairly long chapter that has covered many details about the internal architecture of AVR microcontrollers. Concepts included in this chapter may be new to many readers and the volume of information may be a bit overwhelming at this stage. If you have had trouble understanding everything in this chapter, or it has just been too much information in one go, then either go over the chapter again, or come back to it again later. Remember that if you have never studied the internal workings of any microcontroller or microprocessor before, and this is the first time looking at this kind of material, it will take time to get to understand and remember everything. There is nothing wrong with going over this book two or three times until you understand everything properly.

In the next chapter we look at arithmetic instructions including how positive and negative numbers are stored in memory. Logic instructions are also covered that are essential when manipulating bits in registers which can be used to control internal and external hardware on the microcontroller. This prepares us for many of the chapters that follow that set up and use hardware in the AVR, such as I/O ports and timers.

## Chapter 7 · Arithmetic and Logic Instructions

Arithmetic and logic instructions are processed in the arithmetic and logic unit, or ALU, of the microcontroller core.

ATtiny13(A) and ATtiny25/45/85 microcontrollers have addition and subtraction arithmetic instructions, as well as AND, OR and exclusive OR logical instructions.

This chapter looks at examples of each of the basic mathematical and logical operations, but first looks at how negative numbers are represented in binary.

### In this Chapter

- Positive and negative numbers in binary
- Binary addition and subtraction
- Logic instructions in ATtiny microcontrollers

### 7.1 Positive and Negative Numbers

A positive 8-bit binary number uses all eight bits to represent a positive number with each bit weighted as already explained. This means that a positive 8-bit number can have a value from 0b0000_0000 (0 decimal) to 0b1111_1111 (255 decimal).

A “signed” 8-bit number uses the MSB (left most bit, or bit number 7) as the sign bit which is set to logic 1 to represent a negative number, and cleared to logic 0 to represent a positive number. This means that an 8-bit signed number can have a maximum positive value of 0b0111_1111 (127) and maximum negative number of 0b1111_1111 (-127) when using the MSB for the sign.

An example of a negative 8-bit number is 0b1001_0111 (-23 decimal) where the first digit on the left denotes that the number is negative. The remainder of bits represent the size of the number using the weighted binary numbering system. Positive 23 is represented by changing the sign bit to 0: 0b0001_0111. Microcontrollers usually represent numbers in 2’s compliment (two’s compliment) format, but before we look at 2’s compliment format, we must look at 1’s compliment (one’s compliment) format.

#### 7.1.1 1’s Compliment Numbers

A signed 1’s compliment 8-bit number can be either positive or negative. When it is positive, it is simply a binary number with the left most bit (MSB), or sign bit, with a value of 0 as already explained. When a 1’s compliment number is negative it is the same as the positive version of the number, but with every bit inverted. Inverted means that each 0 in the number is changed to 1 and each 1 is changed to 0. To use the example of +23 and -23 again, 0b0001_0111 is +23 as before. After inverting each bit to represent -23 in 1’s compliment format the number is 0b1110_1000.

#### 7.1.2 2’s Compliment Numbers

Positive numbers in 2’s compliment are the same as 1’s compliment positive numbers and normal binary numbers. Because the maximum value that an 8-bit positive signed number can have is 0b0111_1111 or 127 decimal, incrementing this number by 1 will set the MSB making it a negative number, not 128.

Negative 2’s compliment numbers are the 1’s compliment representation of the number plus one. To convert -23 to 2’s compliment, we first convert the positive version of the

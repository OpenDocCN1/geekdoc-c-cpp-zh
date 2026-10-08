
be used. This instruction will load 0FH into BSR, and will select bank number F. All data registers in bank F will now become active.

However, sometimes the need for bank switching creates a major problem for the programmer. Obviously, programs will not work if the programmer forgets about bank switching. To facilitate access for the most commonly used data memory locations, the data memory is configured with an “Access Bank”, which allows users to access a mapped block of memory without bank switching. As mentioned before, the lower half is known as the “Access RAM” and is comprised of GPRs. This upper half is also where the device’s SFRs are mapped. These two areas are mapped contiguously in the Access Bank and can be addressed in a linear fashion by an 8-bit address (Figure 5.7). It is convenient to use access bank for file registers. The user does not have to worry about bank switching. Hence, one should use access bank whenever possible. Note that upon power-up, the PIC18F uses the

### TABLE 5.1
Selected Special Function Registers (SFRs)

| Address | Name | Description |
| :------- | :----- | :----------------------------------------------------------- |
| 0xFF | TOSU | Top of stack (Upper 5 bits) |
| 0xFFE | TOSH | Top of stack (High byte) |
| 0xFFD | TOSL | Top of stack (Low byte) |
| 0xFFC | STKPTR | Stack Pointer |
| 0xFFB | PCLATU | Program Counter Latch (Upper 5 bits) |
| 0xFFA | PCLATH | Program Counter Latch (Upper byte) |
| 0xFF9 | PCL | Program Counter Latch (Lower byte) |
| 0xFF8 | TBLPTRU | Table Pointer (Upper 5 bits) |
| 0xFF7 | TBLPTRH | Table Pointer (High byte) |
| 0xFF6 | TBLPTRL | Table Pointer (Low byte) |
| 0xFF5 | TABLAT | Table Latch |
| 0xFF4 | PRODH | Product Register (High byte) |
| 0xFF3 | PRODL | Product Register (Low byte) |
| 0xFE | INDF0(1) | Indirect File Register 0; associated with FSR0 |
| 0xFEE | POSTINC0(1) | Postincrement Pointer 0; uses FSR0 |
| 0xFED | POSTDEC0(1) | Postdecrement Pointer 0; uses FSR0 |
| 0xFEC | PREINC0(1) | Predecrement Pointer 0; uses FSR0 |
| 0xFEB | PLUSW0(1) | Add FSR0 to WREG and uses as pointer for data registers |
| 0xFE | FSR0H | File Select Register 0 (High byte) |
| 0xFE9 | FSR0L | File Select Register 0 (Low byte) |
| 0xFE8 | WREG | Working Register (Accumulator) |
| 0xFE7 | INDF1(1) | Indirect File Register 1; associated with FSR1 |
| 0xFE6 | POSTINC1(1) | Postincrement Pointer 1; uses FSR1 |
| 0xFE5 | POSTDEC1(1) | Postdecrement Pointer 1; uses FSR1 |
| 0xFE4 | PREINC1(1) | Predecrement Pointer 1; uses FSR1 |
| 0xFE3 | PLUSW1(1) | Add FSR1 to WREG and uses as pointer for data registers |
| 0xFE2 | FSR1H | File Select Register 1 (High byte) |
| 0xFE1 | FSR1L | File Select Register 1 (Low byte) |
| 0xFE0 | BSR | Branch Select Register |
| 0xFD | FSR2H | File Select Register 2 (High byte) |
| 0xFD9 | FSR2L | File Select Register 2 (Low byte) |
| 0xFD8 | SR | Status Register |

**Note 1:** This is not a physical register.

access bank of the file registers as the default bank. In the core PIC18F instruction set, only the MOVFF instruction fully specifies the 12-bit address of the source and target registers. The size of this instruction is two words. This instruction ignores the BSR completely when it executes. All other instructions include only the low-order address as an operand and must use either the BSR or the Access Bank to locate their target registers.

## 5.4 PIC18F Addressing Modes

Most instructions contain one or more operands. Some instructions have no operands. The manner in which a microcontroller specifies location(s) of operand(s) and destination addresses is called the “addressing mode”. Note that an operand may be immediate data (literal), or data stored in a register or in data memory.

The PIC18F provides six addressing modes:

- 1. Literal or Immediate Addressing Mode
- 2. Inherent or Implied Addressing Mode
- 3. Direct or Absolute Addressing Mode
- 4. Indirect Addressing Mode
- 5. Relative Addressing Mode
- 6. Bit Addressing Mode

An additional addressing mode, Indexed Literal Offset, is available when the extended instruction set is enabled. However, this mode will not be described here.

### 5.4.1 Literal or Immediate Addressing Mode

In the literal or immediate mode, the operand data is a literal or constant data. Immediate data is part of the instruction. This means that the data follows the opcode after assembling an instruction with immediate addressing mode. Constant data can be moved into the WREG or any other specified register such as BSR. However, constant data cannot be moved into file registers using the Literal or Immediate mode. This mode can also be used by PIC18F arithmetic and logic instructions to be covered in Chapter 6.

An example is the MOVLW 0x2A instruction in which MOVLW uses immediate mode, and moves 8-bit data 2AH into the WREG register.

### 5.4.2 Inherent or Implied Addressing Mode

In the inherent or implied mode, instructions do not require operands. These instructions are also called no-operand instructions. An example of an instruction with inherent or implied mode is the DAW instruction. The DAW is a no-operand instruction. It adjusts the sum (adds 6 for BCD correction) in the WREG register stored after addition of two 8-bit packed BCD numbers. Note that the DAW instruction implicitly or inherently uses the WREG register .

### 5.4.3 Direct or Absolute Addressing Mode

In the direct or absolute addressing mode, the address is included as part of the instruction. This address specifies either a data register address in one of the banks of data SRAM or a location in the Access Bank as the data source for the instruction. Direct addressing mode specifies all or part of the source and/or destination address of the operation within the opcode itself.

An example of the direct addressing mode is MOVWF 0x50. Note that the letter F in the instruction MOVWF indicates the address of the file register in direct addressing mode, and “0x” means hexadecimal number.

The MOVWF 0x50 instruction moves the contents of the WREG register into a file register in the data SRAM whose address is 0x50. The contents of WREG are unchanged. MOVWF 0x50 uses direct address mode since address 0x50 is directly specified in the MOVWF instruction.

Note that the 12-bit address, 0x050 in the access bank, is specified by 8-bit number 0x50 in the MOVWF instruction since the upper four bits (0H) of the 12-bit address 0x050 specify the bank number 0 (access bank) in this case. The 8-bit address (0x50) is included in the MOVWF (16-bit wide) instruction. As mentioned before, in the PIC18F, addresses are specified as 8-bit numbers while the bank number is specified by the access bank or BSR.

### 5.4.4 Indirect Addressing Mode

In *Indirect Addressing Mode*, a register is used as a pointer to an address in the data memory. In the PIC18F, three registers, namely FSR0, FSR1, and FSR2 are used for this purpose. Note that “FSR” stands for file select register. The PIC18F CPU contains these registers. As mentioned before, each of these 16-bit registers is divided into low byte and high byte as follows: FSR0 as FSR0H and FSR0L, FSR1 as FSR1H and FSR1L, FSR2 as FSR2H and FSR2L. Each of these registers holds a 12-bit memory address to point to a data memory location. Since FSR’s are 16-bit wide, the 12-bit address is stored in low 12 bits (bits 0 through 11) of the FSRs with the upper four bits (bits 12 through 15) as 0’s.

Each FSR is associated with an SFR (Special Function Register) called INDF (Indirect File) as follows: FSR0 is associated with SFR called INDF0, FSR1 is associated with SFR called INDF1, and FSR2 is associated with SFR called INDF2. The FSR’s can be initialized using the LFSR (Load FSR) instruction. The following examples illustrate this:

```
LFSR    0, 0x00010    ; Load  0010H into FSR0
LFSR    1, 0x0040     ; Load  0040H into FSR1
LFSR    2, 0x0080     ; Load  0080H into FSR2
```

After initializing one of the FSR’s, data can be moved into a RAM location indirectly using the associated SFR called INDF. For example, in order to move the

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_116_0.png)

(a) Memory contents after execution of MOVLW and LFSR instructions in the example for indirect addressing

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_116_1.png)

(b) Memory contents after execution of MOVWF in the example for indirect addressing

**FIGURE 5.8** Illustration of the Indirect Addressing Mode

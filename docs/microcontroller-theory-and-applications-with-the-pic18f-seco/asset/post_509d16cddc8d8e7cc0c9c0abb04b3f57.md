
## Appendix C: PIC18F Instruction Set (Alphabetical Order)

| Instruction | Example | Operation |
| :--- | :--- | :--- |
| BTFC F, b, a | BTFC 0x50, 3 | If bit number 3 in data register 0x50 is 0, skip the next instruction; otherwise, the next instruction is executed. |
| BTFS F, b, a | BTFS 0x40, 0 | If bit number 0 in data register 0x40 is 1, skip the next instruction; otherwise, the next instruction is executed. |
| BTG F, b, a | BTG 0x20, 2 | Invert (ones complement) bit number 2 in data register 0x20. |
| BZ d8 | BZ START | Branch to START if Z = 1 where START is an 8-bit signed number. |
| CALL k, s | CALL BEGIN | This is a two-word instruction. The simplest way to CALL a subroutine is when s = 0 (default); pushes current program counter (PC+4) which is also the return address, and loads PC with BEGIN which is the starting address of the subroutine. |
| CLRF F, a | CLRF 0x40 | Clear the contents of data register to 0. |
| CLRWDT | CLRWDT | Reset the watchdog timer. |
| COMF F, d, a | COMF 0x30, F | One's complement each bit of [0x30], and store the result in 0x30. |
| | COMF 0x30, W | One's complement each bit of [0x30], and store the result in WREG. |
| CPFSEQ F, a | CPFSEQ 0x30 | Unsigned comparison. If [0x30] = [WREG], skip the next instruction; else, the next instruction is executed. |
| CPFSGT F, a | CPFSGT 0x50 | Unsigned comparison. If [0x50] > [WREG], skip the next instruction; else, the next instruction is executed. |
| CPFSLT F, a | CPFSLT 0x60 | Unsigned comparison. If [0x60] < [WREG], skip the next instruction; else, the next instruction is executed. |
| DAW | DAW | Decimal Adjust [WREG] resulting from earlier addition of two packed BCD digits providing correct packed BCD result. |
| DECF F, d, a | DECF 0x20, W | Decrement [0x20] by 1, and store result in WREG. |
| | DECF 0x20, F | Decrement [0x20] by 1, and store result in 0x20. |
| DECFSZ F, d, a | DECFSZ 0x30, W | Decrement [0x30] by 1, and store result in WREG. If [WREG] = 0, skip the next instruction; else, execute the next instruction. |
| | DECFSZ 0x30, F | Decrement [0x30] by 1, and store the result in 0x30. If [0x30] = 0, skip the next instruction; else, execute the next instruction. |
| DECFSNZ F, d, a | DECFSNZ 0x50, W | Decrement [0x50] by 1, and store result in WREG. If [WREG] ≠ 0, skip the next instruction; else, execute the next instruction. |
| | DECFSNZ 0x50, F | Decrement [0x50] by 1, and store the result in 0x50. If [0x50] ≠ 0, skip the next instruction; else, execute the next instruction. |
| GOTO k | GOTO START | Unconditional branch to address *START*. |
| INCF F, d, a | INCF 0x20, W | Increment [0x20] by 1, and store result in WREG. |
| | INCF 0x20, F | Increment [0x20] by 1, and store result in 0x20. |
| INCFSZ F, d, a | INCFSZ 0x30, W | Increment [0x30] by 1, and store result in WREG. If [WREG] = 0, skip the next instruction; else, execute the next instruction. |
| | INCFSZ 0x30, F | Increment [0x30] by 1, and store the result in 0x30. If [0x30] = 0, skip the next instruction; else, execute the next instruction. |
| INCFSNZ F, d, a | INCFSNZ 0x50, W | Increment [0x50] by 1, and store result in WREG. If [WREG] ≠ 0, skip the next instruction; else, execute the next instruction. |
| | INCFSNZ 0x50, F | Increment [0x50] by 1, and store the result in 0x50. If [0x50] ≠ 0, skip the next instruction; else, execute the next instruction. |
| IORLW k | IORLW 0x54 | The contents of WREG are logically ORed with 0x54, and the result is stored in WREG. |
| IORWF F, d, a | IORWF 0x50, W | The contents of WREG are logically ORed with the contents of 0x50, and the result is stored in WREG. |
| | IORWF 0x50, F | The contents of WREG are logically ORed with the contents of 0x50, and the result is stored in 0x50. |
| LFSR F, k | LFSR 0, 0x0080 | Load 00H into FSR0H, and 80H into FSR0L. |
| MOVF F, d, a | MOVF 0x30, W | The contents of 0x30 are loaded into WREG. |
| | MOVF 0x30, F | The contents of 0x30 are copied into 0x30. |
| MOVFF Fs, Fd | MOVFF 0x50, 0x60 | Move [0x50] into [0x60]. The contents of 0x50 are unchanged. |
| MOVLB k | MOVLB 0x04 | Load BSR with 04H. |
| MOVLW k | MOVLW 0x21 | Load WREG with 21H. |
| MOVWF F, a | MOVWF 0x50 | Move the contents of WREG into 0x50. |
| MULLW k | MULLW 0xF1 | [WREG] x F1H → [PRODH] [PRODL]; unsigned multiplication. |
| MULWF F, a | MULWF 0x30 | [WREG] x [0x30] → [PRODH] [PRODL]; unsigned multiplication. |
| NEGF F, a | NEGF 0x20 | Negate the contents of 0x20 using two's complement. |
| NOP | NOP | No Operation. |
| POP | POP | Discard top of stack pointed by SP, and decrement PC by 1. |
| PUSH | PUSH | Push or write PC onto the stack, and increment SP by 1. |
| RCALL n | RCALL START | Relative subroutine CALL. One-word instruction. Pushes PC+2 onto the hardware stack. START is an 11-bit signed number. Jumps to a subroutine located at an address (PC + 2) + 2 x START. |
| RESET | RESET | Reset all registers and flags that are affected by a MCLR reset. |
| RETFIE | RETFIE | Return from Interrupt. |
| RETLW k | RETLW k | WREG is loaded with the 8-bit literal k, and PC is loaded with the return address from the top of stack. |
| RETURN | RETURN | Return from subroutine. |
| RLCF F, d, a | RLCF 0x20, W | Rotate [0x20] once to the left through Carry. Store result in WREG. |
| | RLCF 0x20, F | Rotate [0x20] once to the left through Carry. Store result in register 0x20. |
| RLNCF F, d, a | RLNCF 0x30, W | Rotate [0x30] once to the left without Carry. Store result in WREG. |
| | RLNCF 0x30, F | Rotate [0x30] once to the left without Carry. Store result in register 0x30. |
| RRCEF F, d, a | RRCEF 0x50, W | Rotate [0x50] once to the right through Carry. Store result in WREG. |
| | RRCEF 0x50, F | Rotate [0x50] once to the right through Carry. Store result in register 0x50. |
| RRNCF F, d, a | RRNCF 0x60, W | Rotate [0x60] once to the right without Carry. Store result in WREG. |
| | RRNCF 0x60, F | Rotate [0x60] once to the right without Carry. Store result in register 0x60. |
| SETF F, a | SETF 0x30 | The contents of 0x30 are set to 1's. |
| SLEEP | SLEEP | Enter Sleep mode. |
| SUBFWB F, d, a | SUBFWB 0x20, W | [WREG] – [0x20] – Carry → [WREG] |
| | SUBFWB 0x20, F | [WREG] – [0x20] – Carry → [0x20] |
| SUBLW k | SUBLW 0x05 | [0x05] – [WREG] → [WREG] |
| SUBWF F, d, a | SUBWF 0x50, W | [0x50] – [WREG] → [WREG] |
| | SUBWF 0x50, F | [0x50] – [WREG] → [0x50] |
| SUBWFB F, d, a | SUBWFB 0x32, W | [0x32] – [WREG] – Carry → [WREG] |
| | SUBWFB 0x32, F | [0x32] – [WREG] – Carry → [0x32] |
| SWAPF F, d, a | SWAPF 0x30, W | The upper and lower 4 bits of register 0x30 are exchanged. The result is stored in WREG. |
| | SWAPF 0x30, F | The upper and lower 4 bits of register 0x30 are exchanged. The result is stored in register 0x30. |
| TBLRD | TBLRD | Table Read. |
| TBLWT | TBLWT | Table Write. |
| TSTFSZ F, a | TSTFSZ 0x50 | If [0x50] = 0, skip the next instruction; else, execute the next instruction. |
| XORLW k | XORLW 0xF2 | [WREG] XOR F2h → [WREG] |
| XORWF F, d, a | XORWF 0x30, W | [WREG] XOR [0x30] → [WREG] |
| | XORWF 0x30, F | [WREG] XOR [0x30] → [0x30] |

## APPENDIX D: PIC18F INSTRUCTION SET — DETAILS

### 24.0 INSTRUCTION SET SUMMARY

PIC18F4321 family devices incorporate the standard set of 75 PIC18 core instructions, as well as an extended set of 8 new instructions, for the optimization of code that is recursive or that utilizes a software stack. The extended set is discussed later in this section.

### 24.1 Standard Instruction Set

The standard PIC18 instruction set adds many enhancements to the previous PIC18 instruction sets, while maintaining an easy migration from these PIC instruction sets. Most instructions are a single program memory word (16 bits), but there are four instructions that require two program memory locations.

Each single-word instruction in structure is a 16-bit word divided into an opcode, which specifies the instruction type, and one or more operands, which further specify the operation of the instruction.

The instruction set is highly orthogonal and is grouped into four basic categories:

- Byte-oriented operations
- Bit-oriented operations
- Literal operations
- Control operations

The PIC18 instruction set summary in Table 24-2 lists byte-oriented, bit-oriented, literal, and control operations. Table 24-1 shows the opcode field descriptions.

Most byte-oriented instructions have three operands:
1. The file register (specified by ‘f’)
2. The destination of the result (specified by ‘d’)
3. The accessed memory (specified by ‘a’)

The file register designator ‘f’ specifies which file register is to be used by the instruction. The destination designator ‘d’ specifies where the result of the operation is to be placed. If ‘d’ is zero, the result is placed in the WREG register. If ‘d’ is one, the result is placed in the file register specified in the instruction.

All bit-oriented instructions have three operands:
1. The file register (specified by ‘f’)
2. The bit in the file register (specified by ‘b’)
3. The accessed memory (specified by ‘a’)

The bit file designator ‘b’ selects the number of the bit affected by the operation, while the file register designator ‘f’ represents the number of the file in which the bit is located.

The literal instructions may use some of the following operands:
- A literal value to be loaded into a file register (specified by ‘k’)
- The desired FSR register to load the literal value into (specified by ‘t’)
- No operand required (specified by ‘–’)

The control instructions may use some of the following operands:
- A program memory address (specified by ‘n’)
- The mode of the CALL or RETURN instructions (specified by ‘s’)
- The mode of the table read and table write instructions (specified by ‘m’)
- No operand required (specified by ‘–’)

All instructions are a single word, except for two double-word instructions. The six instructions were made double-word to contain the required information in 32 bits. In the second word, the 4 MSBs are ‘2’s. If this second word is executed as an instruction (by itself), it will execute as a NOP.

All non IWL-locked instructions are executed in a single instruction cycle, unless a conditional test is true or the program counter is changed as a result of the instruction. In these cases, the execution takes two instruction cycles, with the additional instruction cycle(s) executed as a NOP. The double-word instructions execute in two instruction cycles.

One instruction cycle consists of four oscillator periods. Thus, for an oscillator frequency of 4 MHz, the normal instruction execution time is 1 µs. If a conditional test is true, or the program counter is changed as a result of an instruction, the instruction execution time is 2 µs. Two-word branch instructions (if true) would take 3 µs.

Figure 24-1 shows the general formats that the instructions can have. All examples use the convention ‘nnh’ to represent a hexadecimal number.

The Instruction Set Summary, shown in Table 24-2, lists the standard instructions recognized by the Microchip MPASM™ Assembler.

Section 24.1.1 “Standard Instruction Set” provides a description of each instruction.

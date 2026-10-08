
GOTO NEXT  
GOTO REPEAT ; Repeat addition until counter 0x60 is 0  
NEXT ; Next instruction  

Using the DECFSZ, the above program to compute (10 x A) can be written as follows:

```
CLRF 0x50 ; Clear register 0x50 to 0 for SUM
MOVW D'10' ; Move 10 to WREG
MOVWF 0x60 ; Initialize register 0x60 with 10
MOVF 0x70,W ; Move 'A' into WREG
REPEAT ADDWF 0x50, F ; Add 'A' 10 times, store result in 0x50
 DECFSZ 0x60, F ; Decrement counter, skip if 0
 GOTO REPEAT ; Repeat addition until counter 0x60 is 0
 ; Next instruction
```

- **INCFSNZ or INCFSZ F, d, a** (INCFSNZ or INCFSZ 0x40, W or 0x40, F) increments the contents of register 'F' by one, and skips the next instruction if the result is not 0; else, the next instruction is executed. The INCFSZ F, d, a, on the other hand, increments the contents of register 'F' by one, and skips the next instruction if the result is 0; else, the next instruction is executed. The GOTO or BRA instruction is typically used after each of these instructions.

Both instructions can be used to execute a certain loop 'n' times, where 'n' is an 8-bit number. This is another way of executing a loop without using the conditional branch instructions.

Consider the same examples of the last section using the DECFSNZ and DECFSZ instructions. As before, a loop will be executed to obtain the 8-bit SUM (10 x A) by repeated addition, assuming that the 8-bit unsigned number, 'A', is stored in register 0x70, and the SUM will be stored in 0x50. The INCFSNZ and INCFSZ will be used this time.

The following PIC18F instruction sequence using INCFSNZ will accomplish this:

```
CLRF 0x50 ; Clear register 0x50 to 0 for SUM
MOVW 0xF6 ; Move -10 to WREG
MOVWF 0x60 ; Initialize register 0x60 with -10
MOVF 0x70,W ; Move 'A' into WREG
REPEAT ADDWF 0x50, F ; Add 'A' 10 times, store result in 0x50
 INCFSNZ 0x60, F ; Increment counter, skip if reg 0x60 not 0
 GOTO NEXT
 GOTO REPEAT ; Repeat addition until counter 0x60 is 0
NEXT ; Next instruction
```

Using the INCFSZ, the above program to compute (10 x A) can be written as follows:

```
CLRF 0x50 ; Clear register 0x50 to 0 for SUM
MOVW 0xF6 ; Move -10 to WREG
MOVWF 0x60 ; Initialize register 0x60 with -10
MOVF 0x70,W ; Move 'A' into WREG
REPEAT ADDWF 0x50, F ; Add 'A' 10 times, store result in 0x50
 INCFSZ 0x60, F ; Increment counter, skip if counter is 0
GOTO REPEAT ; Repeat addition until counter 0x60 is 0
 ; Next instruction
```

- **TSTFSZ** F, a (**TSTFSZ 0x60**) checks if [F] = 0, and skips the next instruction if it is zero (*Z* = 1); otherwise (*Z* = 0), the next instruction is executed. The **TSTFSZ** instruction can be used to check the contents of a register for 0 without using the conditional branch instruction. For example, a typical decrementing counter can be implemented using the conditional branch instruction such as **BNZ** as follows:

```
COUNTER EQU 0x40
 MOVLW D'50' ; Initialize loop counter with 50
 MOVWF COUNTER
LOOP DECf COUNTER ; Decrement COUNTER by 1
 BNZ LOOP
 ; Branch if [COUNTER] is not 0
 ; Next instruction
```

The above loop can be implemented using the TSTFSZ instruction as follows:

```
COUNTER EQU 0x40
 MOVLW D'50' ; Initialize loop counter with 50
 MOVWF COUNTER
LOOP DECf COUNTER ; Decrement COUNTER by 1
 TSTFSZ COUNTER ; Test COUNTER for 0 and if not 0,
GOTO LOOP ; go to LOOP. If [COUNTER] is 0, skip.
 ; Next instruction
```

## Example 7.1

Write a *PIC18F* assembly language program at 0x100 to subtract two 32-bit numbers as follows:

```
[0x43] [0x42] [0x41] [0x40]
MINUS [0x75] [0x74] [0x73] [0x72]
----------------------
     [0x43] [0x42] [0x41] [0x40]
```

Assume data registers 0x40 through 0x43 contain the first 32-bit number while data registers 0x72 through 0x75 contain the second 32-bit number. Also, assume that data are already loaded into the data registers. Store the 32-bit result in data registers 0x40 (lowest byte) through 0x43 (highest byte). Use a loop. This is Example 6.12 using a loop.

### *Solution*

```
INCLUDE <P18F4321.INC>
ORG 0x100
MOVLW 4 ; Move WREG with 4
MOVWF 0x50 ; Initialize 0x50 with loop count (4)
LSFR 0, 0x0072 ; Initialize pointer FSR0 with 0x0072
LSFR 1, 0x0040 ; Initialize pointer FSR1 with 0x0040
ADDLW 0x00 ; Clear carry flag
START MOVF POSTINC0, W ; Move byte into WREG and update pointer
SUBWFB POSTINC1, F ; Subtract [WREG] and carry from byte.
; store result in data register
DECFSZ 0x50,F ; Decrement counter 0x50 by 1 and skip if [0x50] = 0
BNZ START ; Branch to START if Z is 0
SLEEP ; Halt
END
```

Note: In the above, DECFSZ is used instead of DEC F. This is because DECF affects the carry flag while DECFSZ does not.

## 7.3 PIC18F Table Read/Write instructions

As mentioned before, the PIC18F program memory is 16 bits wide, while the PIC18F data memory space is 8 bits wide. Programs are stored in program memory with the data register contents defined using the assembler's DB directive. In order to execute a program requiring data, the data bytes stored in program memory using DB directive must be transferred to the specified data registers in data memory. Since the sizes of program memory and data memory are different, it would be difficult to accomplish this data transfer.

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_172_0.png)

FIGURE 7.1 Table Read Operation (Instruction TBLRD*)

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_172_1.png)

FIGURE 7.2 Table Write Operation (Instruction TBLWT*)

However, four table read and four table write instructions provided in the PIC18F facilitate transferring data between these two memory spaces through an 8-bit TABLAT (register called Table latch), and a 21-bit TBLPTR (pointer register called the Table pointer). The TBLPTR includes three registers, namely TABLPRR (bits 20 through 16), TBLPTRH (bits 15 through 8), and TBLPTRL (bits 7 through 0). Since the PIC18F4321 uses 13-bit program address, the low 13 bits of the TBLPTR will be used as the pointer, and upper bits of TBLPTR will be 0's.

Two operations that allow the PIC18F to move bytes between the program memory and the data memory:

- Table Read (TBLRD)
- Table Write (TBLWT)

Table read operation retrieves data from program memory and places it into the data memory. Figure 7.1 shows the operation of a table read with program memory and data memory. The Table read operation is accomplished using the TBLRD instruction with four addressing modes (register indirect, postincrement, postdecrement, and predecrement).

Table write operation stores data from the data memory space into holding registers in program memory. Figure 7.2 shows the operation of a table write with program memory and data memory. The Table write operation is accomplished using the TBLWT instruction with four addressing modes (register indirect, postincrement, postdecrement, and predecrement). Table operations work with data bytes. A table block containing data, rather than program instructions, is not required to be word aligned. Therefore, a table block can start and end at any byte address. Note that although the TBLPTR is 21-bit wide, the PIC18F4321 uses low 13 bits of the 21-bit address since the PIC18F4321 program memory address is 13-bit wide.

Table 7.3 lists the TBLRD and TBLWT instructions.

| Instruction | Description |
| :--- | :--- |
| TBLRD* | Move 8-bit data from program memory addressed by 21-bit TBLPTR into the 8-bit register TABLAT. |
| TBLRD*+ | Move 8-bit data from program memory addressed by 21-bit TBLPTR into the 8-bit register TABLAT, and then increment TBLPTR by 1. |
| TBLRD*- | Move 8-bit data from program memory addressed by 21-bit TBLPTR into the 8-bit register TABLAT, and then decrement TBLPTR by 1. |
| TBLRD+* | Increment TBLPTR by 1 and then move 8-bit data from program memory addressed by 21-bit TBLPTR into the 8-bit register TABLAT. |
| TBLWT* | Move 8-bit data from 8-bit register TABLAT into program memory addressed by 21-bit TBLPTR. |
| TBLWT*+ | Move 8-bit data from 8-bit register TABLAT into program memory addressed by 21-bit TBLPTR, and then increment TBLPTR by 1. |
| TBLWT*- | Move 8-bit data from 8-bit register TABLAT into program memory addressed by 21-bit TBLPTR, and then decrement TBLPTR by 1. |
| TBLWT+* | Increment TBLPTR by 1 and then move 8-bit data from 8-bit register TABLAT into program memory addressed by 21-bit TBLPTR. |

- All TBLRD and TBLWT instructions are executed in two cycles.
- The size of each instruction is one word.

The table read/write instructions will now be explained in the following using numerical examples with similar data for each instruction:

- Consider TBLRD* instruction.

Prior to execution of TBLRD* : [TBLPTR] = 0x000128, [TABLAT] = 0x24, [0x000128] = 0xF2.

After execution of TBLRD*: [TABLAT] = 0xF2, [TBLPTR] = 0x000128 (unchanged), [0x000128] = 0xF2 (unchanged)

- Consider TBLRD*+ instruction.

Prior to execution of TBLRD*+: [TBLPTR] = 0x000040, [TABLAT] = 0x24, [0x000040] = 0xF2

After execution of TBLRD*+: [TABLAT] = 0xF2, [TBLPTR] = 0x000041, [0x000040] = 0xF2 (unchanged)

- Consider TBLRD*- instruction.

Prior to execution of TBLRD*-[TABLAT] = 0x000051, [0x000052] = 0xF2 (unchanged)

After execution of TBLRD*-[TABLAT] = 0xF2, [TBLPTR] = 0x000051, [0x000052] = 0xF2 (unchanged)

- Consider TBLRD+* instruction.

Prior to execution of TBLRD+*: [TBLPTR] = 0x000030, [TABLAT] = 0x24, [0x000031] = 0xF2

After execution of TBLRD+*: [TABLAT] = 0xF2, [TBLPTR] = 0x000031, [0x000031] = 0xF2 (unchanged)

- Consider TBLWT* instruction.

Prior to execution of TBLWT*:[TBLPTR] = 0x000120, [TABLAT] = 0x24, [0x000120] = 0x14

After execution of TBLWT*:[0x000120] = 0x24, [TABLAT] = 0x24 (unchanged), [TBLPTR] = 0x000120 (unchanged)

- Consider TBLWT*+ instruction.

Prior to execution of TBLWT*+: [TBLPTR] = 0x000030, [TABLAT] = 0x1F, [0x000030] = 0x02

After execution of TBLWT*+: [0x000030] = 0x1F, [TBLPTR] = 0x000031, [TABLAT] = 0x1F (unchanged)

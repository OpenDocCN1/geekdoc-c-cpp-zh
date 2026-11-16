# 5.69 LDI – Load Immediate

# 5.69.1 Description

Loads an 8-bit constant directly to register 16 to 31.

| Registers and Operands |
| :--- |
| Rd: Destination (and source) register in the Register File |
| K: Constant data |

+   - Operation: Rd = K
+   - Syntax: LDI Rd,K
+   - Operands: 16 ≤ d ≤ 31, 0 ≤ K ≤ 255
+   - Program Counter: PC ← PC + 1

| 16-bit Opcode: |
| :--- |
| 1110 KKKK dddd KKKK |

# 5.69.2 Status Register (SREG) and Boolean Formula

| I | T | H | S | V | N | Z | C |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| – | – | – | – | – | – | – | – |

```
cbr r11 : Clear & High byte
ldi r20,0x07 ; Set S, low byte to 0x07
ldi r16,0x01 ; Load constant into Program
; memory pointed to by Y
```

+   Words: 1 (2 bytes)

![](bbox=[0.16, 0.46, 0.85, 0.48])

To make the instructions easier to read in memory, right-click on any byte in the Memory window, and then select 2-byte Integer on the menu that pops up. Values in the Memory window are now shown as 16-bit wide, 4 digit hexadecimal values. To make the data easier to read, select 1 in the Columns: field as we have previously done. Remember to click the two small arrows at the right of the Memory window if the Columns field is not visible (refer back to Figure 6.10). Your Memory window should now look like Figure 6.13 on the next page, but without the assembly language instructions that were added for illustrative purposes. If the window width is made bigger, it will look slightly different with the items normally hidden behind the double arrow appearing next to the Memory drop-down list, as the memory window width is expanded.

If we look at the first 16-bit hexadecimal value, displayed as e005 (which is 0xE005) in the Memory window, as can be seen in Figure 6.13, we are looking at the value that represents the first LDI instruction in the program. The next hexadecimal value, e01c, represents, or is the machine code instruction equivalent of the second LDI instruction including its operands. The code listing that follows shows the machine code instructions included in hexadecimal and binary next to each assembly language instruction. The binary numbers are split up into groups of four bits to make them easier to read.
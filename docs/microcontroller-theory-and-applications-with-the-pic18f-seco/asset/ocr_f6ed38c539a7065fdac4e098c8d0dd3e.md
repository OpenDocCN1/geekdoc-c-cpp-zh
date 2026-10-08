# ORIGIN (ORG)

The directive ORG specifies the starting address of a program or data. For example, after assembling the following statements, the MPLAB will place the assembled code for MOVLW 0x50 starting at address 0x100:

```
ORG           0x100
MOVWL         0x50
```

# Equate (EQU)

The EQU assigns a value in its operand field to an address in its label field. This allows the user to assign a numerical value to a symbolic name. The user can then use the symbolic name in the program instead of its numerical value. A typical example of EQU is START EQU 0x20, which assigns the value 20 in hexadecimal to the label START.

To illustrate the EQU directive, consider the following instruction sequence:

```
TEST EQU    0x20
      MOVWL   TEST
      MOVWF   TEST
```

The instruction MOVWL TEST, in the above, moves the constant 0x20 into WREG. The instruction MOVWF TEST, on the other hand, moves the contents of WREG into the data register with address 0x20.

# Define Byte (DB)

The directive DB is generally used to set a memory location to a certain byte value. For example,

```
START DB      0x45
```

will store the data value 45 hex to the address START. The DB directive can be used to generate a table of data as follows:

```
ORG    0x70
DB     0x20,0x30,0x40,0x50
```

In this case, 20 hex is the first data of the memory location 70 hex; 30 hex, 40 hex, and 50 hex occupy the next three memory locations. Therefore, the data in memory will look like this:

| | |
|---|---|
| 70 | 20 |
| 71 | 30 |
| 72 | 40 |
| 73 | 50 |

# Define Word (DW)

The directive DW is typically used to assign a 16-bit value to two memory locations. For example,

```
ORG           0x50
DW            0x4AC2
```

will assign C2 to location 50 hex and 4A to location 51 hex. It is assumed that the assembler will assign the low byte first (C2) and then the high byte (4A). The DW directive can be used to generate a table of 16-bit data as follows:

```
ORG     0x80
DW      0x5000,0x6000, 0x7000
```
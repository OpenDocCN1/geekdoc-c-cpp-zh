
![](img/4b7e9c58cac527296b19b501116daeb1_62_0.png)

Figure 13 SI Format

For example, there is an instruction known as CLI - Compare Logical Immediate. It compares a byte in memory with the immediate byte and sets 2 bits called the Condition Code to indicate if the byte in memory is equal, less than or greater than the immediate operand.

So, if you want to test if a byte in memory has the value character A, the symbolic instruction might be:

```
CLI MEMB,C'A'
```

This instruction compares the byte in memory at the label MEMB with the immediate byte whose value is the letter A. After MEMB is translated to an appropriate base and displacement pair, the instruction might look something like:

```
CLI 64(R13),C'A'
```

The opcode for CLI is 95₁₆ so the machine language instruction for the above would look like:

```
95C1D040
```

where C1₁₆ is the letter A in hex, D₁₆ is the base register and 040₁₆ is the displacement. Note that in the instruction, the I2 operand actually appears first and the first operand D1(B1) appears second.

Some SI instructions such as Halt IO (HIO), Set System Mask (SSM), Start IO (SIO), Test and Set (TS), Test Channel (TCH) and Test IO (TIO) do not use the immediate operand. The Diagnose instruction (no mnemonic) is an SI instruction with no operands.

## 6.7.5 SS Format

SS instructions come in two flavors: those with one 8 bit length field and those with two 4 bit length fields.

### 6.7.5.1 Single 8 Bit Length Field

In SS instructions, both operands are in memory and specified with base/displacement calculated addresses. In addition, there is a one byte field that gives the length of the target operand.

The length byte is a positive integer in the range 1 to 256 in the assembly language format (what the programmer writes). But in the machine language format, the value for the length byte is one less than the assembly code value (0 to 255). During execution, a 0 length is interpreted as a 1, a 1 as 2, and so forth. This permits lengths ranging from 1 to 256 rather than 0 to 255. It was assumed by the system designers that there would be little need to move zero bytes.

SS instructions are six bytes in length and called storage-storage instructions. SS-8 instructions are specified in assembly language format as:

```
OpCode D1(L,B1),D2(B2)
```

where L is an 8 bit length code. An example would be the Move Character (MVC) instruction which copies one or more bytes beginning at the address specified by the second operand to the bytes beginning at the address specified by the first operand. The length field (shown as 20 in this example) contains the number of bytes to be copied:

```
MVC 1000(20,R13),2000(R13)
```

### 6.7.5.2 Two 4 Bit Length Fields

This is really the same format as above except the 8 bit length byte is viewed as two four bit fields. Thus, the instruction has two lengths. As before, the length values stored in the machine language instruction are interpreted as one greater than what is actually present so a 0 means 1 and 1 means 2 and so forth. The maximum length of each operand is 16. The first length field applies to the first operand and the second to the second.

SS-4 instructions are specified as:

```
OpCode D1(L1,B1),D2(L2,B2)
```

where L1 and L2 are the 4 bit length codes associated with operand 1 and operand 2, respectively.

A typical example would be an Add Packed instruction (AP) which performs a BCD or decimal addition between two memory resident operands. The operands can be of different lengths but the first operand, where the result is stored, must be large enough to hold the answer. In the following example, the first operand is 5 bytes and the second is 3:

```
AP 1000(5,R13),2000(3,R13)
```

All SS instructions are 6 bytes in length. The original SS machine language formats are shown in Figure 14.

![](img/4b7e9c58cac527296b19b501116daeb1_64_0.png)

## Figure 14 SS Formats

As can be seen, in one format, the length byte is taken as an unsigned 8 bit number. In the other variation, the length byte is interpreted as two unsigned 4 bit numbers.

The instruction:
```
MVC 100(8,R13),200(R13)
```
Where the opcode of a MVC is D2₁₆ would, in machine language, look like:

```
D207D064D0C8
```

You can see the opcode is D2, the length is 07, the first base is D₁₆, the first displacement is 064₁₆, the second base is D₁₆ and the second displacement is 0C8₁₆.

Notice that the length is not 8. When represented in machine language, the length is always one less. Thus 0 means 1, 1 means 2 and so forth.

As noted, some SS instructions divide the length byte into two 4 bit fields in order to get 2 lengths. This is mainly used with the class of arithmetic instructions known as decimal or packed. For example, the SS instruction Add Decimal (or Add Packed) with the mnemonic AP has two lengths. The length subfields give the length of the first and second operands, respectively. So, a typical AP instruction might look like:

```
AP VAL1(5),VAL2(3)
```

This means to add the three byte field from the second operand (VAL2) to the contents of the 5 byte field specified as the first operand (VAL1) and leave the result in the first operand. Translated to explicit format the above might look like:

```
AP 32(5,R13),64(3,R13)
```

which would, given the opcode of FA₁₆ yield the machine instruction:
where FA₁₆ is the opcode, 4 is the first 4 bit length code (one less than 5, as before), 2 is the second length, D is the first base, 020₁₆ is the first displacement, D is the second base and 040₁₆ is the second displacement.

### 6.7.5.3 Added SS Formats

In later versions of the architecture additional SS formats were added as shown in Figure 15. These tend to be uncommon instructions such as Load Multiple Disjoint (LMD), Shift and Round Decimal (SRP), Move to Primary (MVCP), Move to Secondary (MVCS) and Move With Key (MVCK).

![](img/4b7e9c58cac527296b19b501116daeb1_65_0.png)

Figure 15 Newer SS Formats

## 6.8 Newer Instruction Formats

As time passed, the architecture evolved. The original 24 bit (16 megabyte) address space grew to 31 bits (2 gigabytes) and then to 64 bits (16 exabytes); the original 32 bit general purpose registers became 64 bits and so on. To take advantage of these changes, instructions were added along with new instruction formats. A good example of what happened can be seen in the evolution of the signed, fixed point binary Add instruction.

In the original architecture there were three instructions you could use to add signed binary integers as shown in Table 12. The first two of these, AR and A, add two 32 bit signed fixed point binary values yielding a 32 bit signed fixed point binary result. The AH instruction adds a 16 bit signed fixed point binary value to a 32 bit register value and yields a signed 32 bit binary result.

| Mnemonic | Format | 1st Operand | 2nd Operand | 2nd Operand Displacement | Result | Op Code |
|---|---|---|---|---|---|---|
| AR | RR | 32 bit GPR | 32 bit GPR | N/A | 32 bit GPR | 1A |
| A | RX | 32 bit GPR | 32 bit memory | unsigned 12 bit | 32 bit GPR | 5A |
| AH | RX | 32 bit GPR | 16 bit memory | unsigned 12 bit | 32 bit GPR | 4A |

## Table 12 Original Signed Add Instructions

In the current architecture, however, there are several additional variations of this operation as shown in Table 13.

| Mnemonic | Format | 1st Operand | 2nd Operand | 2nd Operand Displacement | Result | Op Code |
|---|---|---|---|---|---|---|
| AR | RR | 32 bit GPR | 32 bit GPR | N/A | 32 bit GPR | 1A |
| AGR | RRE | 64 bit GPR | 64 bit GPR | N/A | 64 bit GPR | B908 |
| AGFR | RRE | 64 bit GPR | 32 bit GPR | N/A | 64 bit GPR | B918 |
| A | RX | 32 bit GPR | 32 bit memory | unsigned 12 bit | 32 bit GPR | 5A |
| AY | RXY | 32 bit GPR | 32 bit memory | signed 20 bit | 32 bit GPR | E3/5A |
| AG | RXY | 64 bit GPR | 32 bit memory | signed 20 bit | 64 bit GPR | E3/08 |
| AGF | RXY | 64 bit GPR | 32 bit memory | signed 20 bit | 64 bit GPR | E3/18 |
| AH | RX | 32 bit GPR | 16 bit memory | unsigned 12 bit | 32 bit GPR | 4A |
| AHY | RXY | 32 bit GPR | 16 bit memory | signed 20 bit | 32 bit GPR | E3/7A |
| AHI | RI | 32 bit GPR | 16 bit immediate | N/A | 32 bit GPR | A7/8A |

## Table 13 Signed Binary Add Instructions

As can be seen in Table 13, the original three binary add instructions have now grown to ten but not much has really changed. They merely take into account the possibility of several combinations of 32 and 64 bit operands and results along with the newer signed 20 bit displacement. An add instruction with an immediate operand was also added. Note that the original instructions all had eight bit opcodes while the newer instructions use either 16 bit opcodes found in the first 16 bits of the instruction (such as AGR) or an 8 bit opcode in the first 8 bits.

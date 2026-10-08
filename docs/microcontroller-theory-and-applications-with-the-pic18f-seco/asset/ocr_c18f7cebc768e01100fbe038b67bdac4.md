g f e d c b a Hex:
0: 1 0 0 0 0 0 0 = 0x40
1: 1 1 1 1 0 0 1 = 0x79
2: 0 1 0 0 1 0 0 = 0x24
3: 0 1 1 0 0 0 0 = 0x30
4: 0 0 1 1 0 0 1 = 0x19
5: 0 0 0 1 0 0 0 = 0x12
6: 0 0 0 0 0 1 1 = 0x03
7: 1 1 1 1 0 0 0 = 0x78
8: 0 0 0 0 0 0 0 = 0x00
9: 0 0 1 1 0 0 0 = 0x18

Note that for a common-anode seven segment display, a ‘0’ will turn a segment ON and a ‘1’ will turn it OFF. Also, bit 7 of PORTB is assumed to be ‘0’. The above table must be stored in the data memory using MOVLW and MOVWF instructions or using the MPLAB assembler directive DB along with the PIC18F assembly language instruction TBLRD (Table Read) with appropriate addressing mode.

The PIC18F assembly language program is provided in the following:

```
INCLUDE <P18F4321.INC>
ORG 0x70
MOVLW 0x40 ; Store 7-segment codes
MOVWF 0x100
MOVLW 0x79
MOVWF 0x101
MOVLW 0x24
MOVWF 0x102
MOVLW 0x30
MOVWF 0x103
MOVLW 0x19
MOVWF 0x104
MOVLW 0x12
```

![](bbox=[0.2, 0.6, 0.9, 0.88])

**FIGURE 8.17** Figure for Example 8.3
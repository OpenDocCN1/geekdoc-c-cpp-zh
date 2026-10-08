If the bit value Y at bit 2 is 1, then the result is nonzero (Flag Z=0); otherwise, the result is zero (Z=1). The Z flag can be tested using typical conditional branch instructions such as BZ (Branch if Z=1) or BNZ (Branch if Z = 0) to determine whether Y is 0 or 1. This is called masking operation. The AND instruction can also be used to determine whether a binary number is ODD or EVEN by checking the Least Significant Bit (LSB) of the number (LSB=0 for even and LSB=1 for odd).

ANDWF 0x60, W performs the same operation as ANDWF 0x60, F except the result is stored in WREG.

+   * COMF F, d, a (COMF 0x50, W or COMF 0x50, F) instruction complements (one’s) the contents of register 'F'. If 'd' is '0', the result is stored in WREG. If 'd' is '1', the result is stored back in register 'F'. If 'a' is '0', the Access Bank is selected. If 'a' is '1', the BSR is used to select the bank.

For example, consider COMF 0x50, W.
Prior to instruction execution: [0x50] = 0x01, [WREG] = 0x57
After instruction execution: [WREG] = 0xFE, [0x50] = 0x01 (unchanged),
Z = 0, N = 1; No other flags are affected.
Note that COMF 0x50, F is the same as COMF 0x50, F except that the result is stored in WREG.

+   * IORLW data8 (IORLW 0x7F) instruction ORes the contents of WREG with the 8-bit literal (immediate data, data8). The result is placed in WREG. As an example, consider IORLW 0x7F.
Prior to instruction execution: [WREG] = 0x01
After instruction execution: [WREG] = 0x7F (unchanged), Z = 0, N = 0; other flags are not affected.
The OR instruction can typically be used to insert a 1 in a particular bit position of a binary number without changing the values of the other bits. For example, a 1 can be inserted using the OR instruction at bit number 3 of the 8-bit binary number 0 1 1 1 0 0 1 1 without changing the values of the other bits as follows:

```
```
0 1 1 1 0 0 1 1 -- 8-bit number
OR   0 0 0 0 1 0 0 0 -- data for inserting a 1 at bit number 3
------------------
0 1 1 1 1 0 1 1 -- Result
```
```

+   * IORWF F, d, a (IORWF 0x50, W or 0x50, F) instruction ORes [WREG] with register 'F'. If 'd' is '0', the result is placed in WREG. If 'd' is '1', the result is placed back in register 'F'. If 'a' is '0', the Access Bank is selected. If 'a' is '1', the BSR is used to select the bank.

As an example, consider IORWF 0x50, W.
Prior to instruction execution: [WREG] = 0xA2, [0x50] = 0x5D
After instruction execution: [WREG] = 0xFF, [0x50] = 0x5D (unchanged), Z = 0, N = 0; other flags are not affected.

IORWF 0x50, F is the same as the IORWF 0x50, W except that the result is stored in 0x50.

The OR instruction can typically be used to insert a 1 in a particular bit position of a binary number without changing the values of the other bits.
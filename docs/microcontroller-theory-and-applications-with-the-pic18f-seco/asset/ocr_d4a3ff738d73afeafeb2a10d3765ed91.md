# Solution

```
ANDLW 0x0F
```

Note that ANDLW 0x0F instruction logically ANDs 8-bit data in WREG with 0x0F. This operation will clear the upper 4 bits to zero, and retain the lower 4 bits. Thus, the 4-bit unsigned number will be converted to an 8-bit unsigned number.

**Example 6.16** Write a PIC18F assembly language program at address 0x100 to convert a 4-bit signed number stored in the low 4 bits of WREG into an 8-bit signed number in WREG. That is, if the 4-bit signed number is positive, zero-extend to 8 bits. On the other hand, if the 4-bit signed number is negative, sign-extend to 8 bits. Assume the 4-bit signed number is already loaded into WREG. Store result in WREG. Do not use any ROTATE instructions.

+   (a) Flowchart the problem.

+   (b) Convert the flowchart to PIC18F assembly language program starting at address 0x100.

# Solution

+   (a) The flowchart is provided below:

![](bbox=[0.14, 0.45, 0.58, 0.87])
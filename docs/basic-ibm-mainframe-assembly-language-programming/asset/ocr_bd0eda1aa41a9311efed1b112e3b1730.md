+   8. Lines 23 through 32 loop through the non-blank characters moving each non-blank character to the output field WORD until the end of REC is encountered or a blank is found.
+   9. Line 28 compares the address in R3 with the limit address R4 and branches to PRNT if it is greater than or equal (Branch Not Low) the value in the limit register R4.
+   10. Line 30 compares the byte pointed to by R3 with a blank (end of word?) and branches to PRNT if so. Otherwise (line 32), it branches to L1 to move the next character.
+   11. Line 34 prints the word extracted from the input image.
+   12. The MVI on line 35 places a blank in the first byte of WORD and then the MVC on line 36 propagates it across the field (this is called a ripple move) thus blanking out WORD. It does this by moving byte 1 to byte 2, then byte 2 to byte 3, and so forth, thus propagating the first byte, the blank.
+   13. The program branches to LOOP to read a new line.
+   14. Sample input lines are shown in Figure 56. These are placed in a file with the same file name as the program but with the .XRD file extension. Output (not shown) consists of the words TEST1, TEST2 and TEST3 on separate lines, left justified.

A related instruction, Translate and Test Reverse (TRTR) was added in later models. It performs the operation of the TRT but in the reverse direction.

```
TEST1       *
      TEST2       *
TEST3
```

Figure 56 Input Lines

# 13.2.2 Translate

The translate instruction (TR) has characteristics that are similar to the TRT. It has a source string, the first operand, and it has a 256 byte table addressed as the second operand. Like the TRT, each byte, successively, from the source string is used to address a byte in the table at an offset equal to the numeric value of the source string byte.

However, in the translate instruction, the byte from the table replaces the byte in the source string. Also, the translate processes the entire source string and does not halt until all bytes have been processed. It does not set the condition code or alter any registers.
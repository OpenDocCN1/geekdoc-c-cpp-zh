# 23. Programming Examples

The following sections present several short programs that illustrate assembly language code in use.

# 23.1 Simple Calculator

The program in Figure 82 is a simple calculator application that reads in lines, extracts two signed fixed point numbers, and an operation code. The it performs the operation and prints the result. The program functions as follows:

+   1. Line 7 and 8 read a line of input and branch to EXIT when there is no more.
+   2. Line 9 echoes the input to the output file. The start of the output record is INP but the length is the sum of the lengths of INP and IN. IN is the field immediately following INP. Consequently, the XPRNT begins at INP and prints the bytes in INP and IN, inclusive, as they are contiguous.
+   3. The address of the input line is loaded into R1 and the output field is blanked on lines 10 through 12.
+   4. The first number from the input is found and converted from zoned decimal to fixed point binary in line 18. If a properly formatted number is not found, a branch is made to print an error message and the program terminates. R1 is advanced by XDECI to point to the blank following the number scanned. The number scanned is written in zoned format to the output field OUT. Lines 14 through 20 process the second number in the same manner except that the zoned decimal version of the number is written to the output field OUT plus 12 since the first 12 bytes are for the first number - positions 0 through 11.
+   5. Lines 22 through 27 scan for the first non-blank character following the second number. R1 initially is the address of the blank immediately following the second number. It is incremented until a non-blank is found or it exceeds the length of the input string. LIM is the address of the byte immediately after the input sting IN. Note that it is declared with an address data type with the value of * (line 85). The * means the current address.
+   6. Lines 29 and 30 copy the operator and the characters => to the output field.
+   7. Lines 32 through 72 perform the calculation based on the operator, convert the result to zoned decimal and print it. Note that the result is placed in the output field displaced by 29 bytes.
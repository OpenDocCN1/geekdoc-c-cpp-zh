next available position. When items are removed from the stack, the address in R4 will be decremented.

4. The main input character processing loop begins at line 13. This line and several following it examine each character of the input in order to determine how to handle same. On line 13 itself, we test if the byte of input pointed to by R2 is an open parenthesis. If it is not, we branch to label L1. If it is, we increment R2 (line 15) and branch back to the top of the loop (effectively, we ignore the open parenthesis). Note the first operand on the CLI instruction on line 13. It has zero displacement past the address in R2. That is, R2 has the address of the operand. In an SI instruction the first operand is addressed by a combination of displacement and base: D1(B1). In this example, the base position is taken by R2.

5. Line 18 tests for the terminating dollar sign and, if it does, branches out of the loop to print the results.

6. Lines 21 through 28 test if the input character is one of the operators. If it is, we branch to the label OPR. If not, on line 29, we branch around the operator handling section to label L2.

7. At OPR we move the operator character onto the stack. R2 points to the input operator character and R4 points to the next available position in the stack. The MVC on line 31 copies the operator byte from the input string to the stack. Again, the displacements are zero because the registers contain the entire address. The 1 in the first operand is the length. We must provide the length as the assembler cannot calculate an implied length (it needs a label to do this). On lines 32 through 34 we increment the input and stack pointers then branch to the top of the loop for the next input character.

8. On line 36 we test if the input is a close parenthesis. If it is not, we branch to label L3. If it is, we decrement the stack pointer and copy the byte from the stack to the next available byte in the output string (pointed to by R3). Then we increment both the input and output pointers. Note that we needed to decrement the stack pointer first because it always points to the next available position. It needs to be decremented to point to the last used position. After the byte from the stack has been copied to the output, the current position in the stack is no longer in use so the stack pointer (R4) is correct.

9. Finally, beginning at line 44, the only alternative remaining is that the character is an operand which we copy to the output string, increment the input and output pointers and branch to the top of the loop.

10. At line 49 we write out the output string and exit.
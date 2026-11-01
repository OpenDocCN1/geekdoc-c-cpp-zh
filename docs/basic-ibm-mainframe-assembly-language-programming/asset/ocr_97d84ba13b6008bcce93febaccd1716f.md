**Figure 96 PI Iterations**

|  |  | |
|---|---|---|
| 00009993 + | .000100070 | 3.1417927728 |
| 00009995 + | .000100050 | 3.1413925728 |
| 00009997 + | .000100030 | 3.1417926928 |
| 00009999 + | .000100010 | 3.1413926528 |
| 00010001 + | .000099990 | 3.1417926128 |
| 00010001 + | .000099990 | 3.1417926128 |

Figure 96 shows the final 14 lines of output for an execution of 10,001 iterations.

# 23.13 Matrix Multiplication

Figure 97 is a program in C to multiply two matrices. Figure 98 gives an example of this program written in assembly language interspersed with comments from the C program. The assembly code corresponds to the C code with some exceptions.

At the beginning of the program (lines 16 through 30), are a number of pointers and integer counts to correspond to the C program declarations. These are branched around by the Branch instruction on line 12.

Basically, the program reads a line of input which contains the number of rows and columns of the first (A) matrix and second (B) matrix (lines 38 through 47). These values are stored in memory.

The number columns in the A matrix is compared with the number of rows in the B matrix. If they are unequal, the program halts (lines 54 through 59).

The dimensions of the result C matrix are calculated (lines 67 through 70).

The total memory requirements for the A matrix, the B matrix and the C matrix are calculated as the sum of number of rows times the number of columns times 4 (each element is a 4 byte fixed point binary integer) for each of the three matrices (lines 72 through 94). The final result, in R7, is passed to the GETMAIN macro on line 96. GETMAIN requests memory from the system. The result, the address of the area allocated by GETMAIN, is returned in R1. The length and address of the allocated area are stored in GLEN and GADDR.

The matrices are to be stored in the allocated area in row major order. That is, the first row followed by the second row and so forth. Lines 101 through 107 determine, based on lengths previously calculated, the addresses in the allocated area (APTR, BPTR and CPTR) of the first elements of each of the matrices and store the pointers to same in memory.
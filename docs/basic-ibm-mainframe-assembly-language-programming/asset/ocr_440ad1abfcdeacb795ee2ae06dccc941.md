# 20. Debugging (XDUMP, SNAP)

A dump is a snapshot, usually in hexadecimal, of the contents of memory, the registers, the PSW and other information relating to the state of the machine at a given instant. The memory area shown by the dump can either be that of a currently running program or larger. In the early days of computing, dumps were produced on paper and could run to thousands of pages. Now they are written to a file.

A dump is ordinarily produced when a program encounters a run time exception or interrupt. Alternatively, a programmer can explicitly request a dump with either the ASSIST XDUMP macro or the system macro SNAP.

In the case of a dump resulting from an error, the program terminates. When a programmer requests a dump, it is usually for diagnostic reasons and the program may or may not terminate, at the programmer's option.

For example, if the program from Figure 47 were modified to include the XDUMP as shown in Figure 71, the result is the text shown in Figure 72 (long lines truncated).

The contents of a dump consist of one or more of the following:

+   1. The contents of the 16 64-bit general purpose registers R0 through RF (R0 through R15);
+   2. The contents of the 16 64-bit floating point registers F0 through FF (F0 through F15);
+   3. The contents of memory beginning at location 00000000₁₆ through location 000FFFFF₁₆.
+   4. The PSW.
+   5. A save area trace back.

The contents of the general purpose and floating point registers are displayed as 16 hexadecimal digits (corresponding to 8 bytes). Normally, there are four registers displayed per line. For example, the first line for the general purpose registers displays R0, R1, R2 and R3 while the last line displays the contents of registers RC (R12), RD (R13), RE (R14) and RF (R15). A similar pattern is shown for the floating point registers (F0 through FF).

The z390 emulator pre-initializes each byte of each register to F4₁₆, thus the high order 32 bits of the registers may be F4₁₆ if the program only uses 32 bit instructions. The low order 32 bits of a register will be F4₁₆ unless the register was used in the course of the program.
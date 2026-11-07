tion speed. Figure 13.16 shows the **optimized SML** for the program of Fig. 13.13. There are **four fewer** instructions in the optimized code. Modify your compiler to perform the optimization you learned in this exercise.

| Simple program | SML location and instruction | Description |
|---|---|---|
| 5 rem sum 1 to x | *none* | rem ignored |
| 10 input x | 00 &nbsp; +1099 | read x into location 99 |
| 15 rem &nbsp; check y == x | *none* | rem ignored |
| 20 if y == x goto 60 | 01 &nbsp; +2098 | load y (98) into accumulator |
|  | 02 &nbsp; +3199 | sub x (99) from accumulator |
|  | 03 &nbsp; +4211 | branch to location 11 if zero |
| 25 rem &nbsp; increment y | *none* | rem ignored |
| 30 let y = y + 1 | 04 &nbsp; +2098 | load y into accumulator |
|  | 05 &nbsp; +3097 | add 1 (97) to accumulator |
|  |  | 06 &nbsp; +2198 | store accumulator in y (98) |
| 35 rem &nbsp; add y to total | *none* | rem ignored |
| 40 let t = t + y | 07 &nbsp; +2096 | load t from location (96) |
|  | 08 &nbsp; +3098 | add y (98) to accumulator |
|  | 09 &nbsp; +2196 | store accumulator in t (96) |
| 45 rem &nbsp; loop to y == x test | *none* | rem ignored |
| 50 goto 20 | 10 &nbsp; +4001 | branch to location 01 |
| 55 rem &nbsp; output result | *none* | rem ignored |
| 60 print t | 11 &nbsp; +1196 | output t (96) to screen |
| 99 end | 12 &nbsp; +4300 | terminate execution |

**Fig. 13.16**  Optimized code for the program of Fig. 13.13.

# **13.34**  *(Enhancing the Simple Compiler)*

Perform the following modifications to the Simple compiler. Some of these may also require modifications to the Simpletron Simulator program you wrote in Exercise 7.10. Many of these are quite challenging and could require substantial effort.

+   a) Modify the Simpletron’s memory to have 1000 cells (000–999). Modify the compiler to generate machine language appropriate for the 1000-element Simpletron memory.
+   
+   b) Allow the compiler to process floating-point values in addition to integers. The Simpletron Simulator must also be modified to process floating-point values.
+   
+   c) Add support for **unary minus** to specify negative integer values.
+   
+   d) Allow the **modulus operator (%)** to be used in let statements. Modify the Simpletron Machine Language to include a modulus instruction.
+   
+   e) Allow **exponentiation** in a let statement using ^ as the exponentiation operator. Modify the Simpletron Machine Language to include an exponentiation instruction.
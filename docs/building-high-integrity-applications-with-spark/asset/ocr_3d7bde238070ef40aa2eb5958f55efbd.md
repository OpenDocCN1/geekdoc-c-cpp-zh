# 4

# # Dependency Contracts

In this chapter we describe SPARK’s features for describing data dependencies and information flow dependencies in our programs. This analysis offers two major services. First, it verifies that no uninitialized data is ever used. Second, it verifies that all results computed by the program participate in some way in the program’s eventual output – that is, all computations are *effective*.

The value of the first service is fairly obvious. Uninitialized data has an indeterminate value. If it is used, the effect will likely be a runtime exception or, worse, the program may simply compute the wrong output. The value of the second service is less clear. A program that produces results that are not used is at best needlessly inefficient. However, ineffective computations may also be a symptom of a larger problem. Perhaps the programmer forgot to implement or incompletely implemented some necessary logic. The flow analysis done by the SPARK tools helps prevent the programmer from shipping a program that is in reality only partially complete.

It is important to realize, however, that flow analysis by itself will not show your programs to be free from the possibility of runtime errors. Flow analysis is only the first step toward building robust software. It can reveal a significant number of faults, but to create highly robust systems, it is necessary to use proof techniques as described in Chapter 6.

As described in Chapter 1, there are three layers of analysis to consider in increasing order of rigor:

+   1. Show that the program is legal Ada that abides by the restrictions of SPARK where appropriate. The most straightforward way to verify this is by compiling the code with a SPARK-enabled compiler such as GNAT.
+   2. Show that the program has no data dependency or flow dependency errors. Verify this by running the SPARK tools to “examine” each source file.
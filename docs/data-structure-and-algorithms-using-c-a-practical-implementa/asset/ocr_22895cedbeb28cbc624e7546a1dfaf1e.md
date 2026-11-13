# ## 1.4 Complexity of an Algorithm

The complexity of programs can be judged by criteria such as whether it satisfies the original specification task, whether the code is readable. These factors affect the computing time and storage requirement of the program.

# ### Space Complexity

The space complexity of a program is the amount of memory it needs to run to completion. The space needed by a program is the sum of the following components:

+   * A fixed part that includes space for the code, space for simple variables and fixed size component variables, space for constants, etc.
+   * A variable part that consists of the space needed by component variables whose size is dependent on the particular problem instance being solved, and the stack space used by recursive procedures.

# ### Time Complexity

The time complexity of a program is the amount of computer time it needs to run to completion. The time complexity is of two types such as

+   * Compilation time
+   * Runtime

The amount of time taken by the compiler to compile an algorithm is known as compilation time. During compilation time it does not calculate for the executable statements, it calculates only the declaration statements and checks for any syntax and semantic errors.

The run time depends on the size of an algorithm. If the number of instructions in an algorithm is large, then the run time is also large, and if the number of instructions in an algorithm is small, then the time for executing the program is also small. The runtime is calculated for executable statements and not for declaration statements.

The first description of the iterative algorithm for data-flow analysis is from the unpublished technical report of Vysotsky and Wegner [20]. The scientific study of data-flow analysis is said to begin with a pair of papers by Allen [2] and Cocke [3].

The lattice-theoretic abstraction described here is based on the work of Kildall [13]. These frameworks assumed distributivity, which many frameworks do not satisfy. After a number of such frameworks came to light, the monotonicity condition was embedded in the model by [5] and [11].

Partial-redundancy elimination was pioneered by [17]. The lazy-code-motion algorithm described in this chapter is based on [14].

Dominators were first used in the compiler described in [13]. However, the idea dates back to [18].

The notion of reducible flow graphs comes from [2]. The structure of these flow graphs, as presented here, is from [9] and [10]. [12] and [15] first connected reducibility of flow graphs to the common nested control-flow structures, which explains why this class of flow graphs is so common.

The definition of reducibility by $T_1$-$T_2$ reduction, as used in region-based analysis, is from [19]. The region-based approach was first used in a compiler described in [21].

The static single-assignment (SSA) form of intermediate representation introduced in Section 6.2.4 incorporates both data flow and control flow into its representation. SSA facilitates the implementation of many optimizing transformations from a common framework [6].

### 9.10. REFERENCES FOR CHAPTER 9

- 1. Allen, F. E., “Program optimization,” *Annual Review in Automatic Programming* 5 (1969), pp. 239–307.
- 2. Allen, F. E., “Control flow analysis,” *ACM Sigplan Notices* 5:7 (1970), pp. 1–19.
- 3. Cocke, J., “Global common subexpression elimination,” *ACM SIGPLAN Notices* 5:7 (1970), pp. 20–24.
- 4. Cocke, J. and J. T. Schwartz, *Programming Languages and Their Compilers: Preliminary Notes*, Courant Institute of Mathematical Sciences, New York Univ., New York, 1970.
- 5. Cousot, P. and R. Cousot, “Abstract interpretation: a unified lattice model for static analysis of programs by construction or approximation of fixpoints,” *Fourth ACM Symposium on Principles of Programming Languages* (1977), pp. 238–252.
- 6. Cytron, R., J. Ferrante, B. K. Rosen, M. N. Wegman, and F. K. Zadeck, “Efficiently computing static single assignment form and the control dependence graph,” *ACM Transactions on Programming Languages and Systems* 13:4 (1991), pp. 451–490.
- 7. Ershov, A. P., “Alpha — an automatic programming system of high efficiency,” *J. ACM* 13:1 (1966), pp. 17–24.
- 8. Gear, C. W., “High speed compilation of efficient object code,” *Comm. ACM* 8:8 (1965), pp. 483–488.
- 9. Hecht, M. S. and J. D. Ullman, “Flow graph reducibility,” *SIAM J. Computing* 1 (1972), pp. 188–202.
- 10. Hecht, M. S. and J. D. Ullman, “Characterizations of reducible flow graphs,” *J. ACM* 21 (1974), pp. 367–375.
- 11. Kam, J. B. and J. D. Ullman, “Monotone data flow analysis frameworks,” *Acta Informatica* 7:3 (1977), pp. 305–318.
- 12. Kasami, T., W. W. Peterson, and N. Tokura, “On the capabilities of while, repeat, and exit statements,” *Comm. ACM* 16:8 (1973), pp. 503–512.
- 13. Kildall, G., “A unified approach to global program optimization,” *ACM Symposium on Principles of Programming Languages* (1973), pp. 194–206.
- 14. Knoop, J., “Lazy code motion,” *Proc. ACM SIGPLAN 1992 conference on Programming Language Design and Implementation*, pp. 224–234.
- 15. Kosaraju, S. R., “Analysis of structured programs,” *J. Computer and System Sciences* 9:3 (1974), pp. 232–255.
- 16. Lowry, E. S. and C. W. Medlock, “Object code optimization,” *Comm. ACM* 12:1 (1969), pp. 13–22.
- 17. Morel, E. and C. Renvoise, “Global optimization by suppression of partial redundancies,” *Comm. ACM* 22 (1979), pp. 96–103.
- 18. Prosser, R. T., “Application of boolean matrices to the analysis of flow diagrams,” *AFIPS Eastern Joint Computer Conference* (1959), Spartan Books, Baltimore MD, pp. 133–138.
- 19. Ullman, J. D., “Fast algorithms for the elimination of common subexpressions,” *Acta Informatica* 2 (1973), pp. 191–213.
- 20. Vysotsky, V. and P. Wegner, “A graph theoretical Fortran source language analyzer,” unpublished technical report, Bell Laboratories, Murray Hill NJ, 1963.
- 21. Wulf, W. A., R. K. Johnson, C. B. Weinstock, S. O. Hobbs, and C. M. Geschke, *The Design of an Optimizing Compiler*, Elsevier, New York, 1975.

## Chapter 10 Instruction-Level Parallelism

Every modern high-performance processor can execute several operations in a single clock cycle. The “billion-dollar question” is how fast can a program be run on a processor with instruction-level parallelism? The answer depends on:

- 1. The potential parallelism in the program.
- 2. The available parallelism on the processor.
- 3. Our ability to extract parallelism from the original sequential program.
- 4. Our ability to find the best parallel schedule given scheduling constraints.

If all the operations in a program are highly dependent upon one another, then no amount of hardware or parallelization techniques can make the program run fast in parallel. There has been a lot of research on understanding the limits of parallelization. Typical nonnumeric applications have many inherent dependences. For example, these programs have many data-dependent branches that make it hard even to predict which instructions are to be executed, let alone decide which operations can be executed in parallel. Therefore, work in this area has focused on relaxing the scheduling constraints, including the introduction of new architectural features, rather than the scheduling techniques themselves.

Numeric applications, such as scientific computing and signal processing, tend to have more parallelism. These applications deal with large aggregate data structures; operations on distinct elements of the structure are often independent of one another and can be executed in parallel. Additional hardware resources can take advantage of such parallelism and are provided in high-performance, general-purpose machines and digital signal processors. These programs tend to have simple control structures and regular data-access patterns, and static techniques have been developed to extract the available parallelism from these programs. Code scheduling for such applications is interesting

### 10.1. PROCESSOR ARCHITECTURES

| | *i* | *i + 1* | *i + 2* | *i + 3* | *i + 4* |
|---|---|---|---|---|---|
| 1. | IF | | | | |
| 2. | ID | IF | | | |
| 3. | EX | ID | IF | | |
| 4. | MEM | EX | ID | IF | |
| 5. | WB | MEM | EX | ID | IF |
| 6. | | WB | MEM | EX | ID |
| 7. | | | WB | MEM | EX |
| 8. | | | | WB | MEM |
| 9. | | | | | WB |

Figure 10.1: Five consecutive instructions in a 5-stage instruction pipeline

Thus, taken branches introduce a delay in the fetch of the branch target and introduce “hiccups” in the instruction pipeline. Advanced processors use hardware to predict the outcomes of branches based on their execution history and to prefetch from the predicted target locations. Branch delays are nonetheless observed if branches are mispredicted.

#### 10.1.2 Pipelined Execution

Some instructions take several clocks to execute. One common example is the memory-load operation. Even when a memory access hits in the cache, it usually takes several clocks for the cache to return the data. We say that the execution of an instruction is *pipelined* if succeeding instructions not dependent on the result are allowed to proceed. Thus, even if a processor can issue only one operation per clock, several operations might be in their execution stages at the same time. If the deepest execution pipeline has n stages, potentially n operations can be “in flight” at the same time. Note that not all instructions are fully pipelined. While floating-point adds and multiplies often are fully pipelined, floating-point divides, being more complex and less frequently executed, often are not.

Most general-purpose processors dynamically detect dependences between consecutive instructions and automatically stall the execution of instructions if their operands are not available. Some processors, especially those embedded in hand-held devices, leave the dependence checking to the software in order to keep the hardware simple and power consumption low. In this case, the compiler is responsible for inserting “no-op” instructions in the code if necessary to assure that the results are available when needed.

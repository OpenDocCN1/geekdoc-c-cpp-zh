# # 21 Iterating in Parallel

In Chapter 19, we mentioned how the cost of computation is falling, resulting in computers with faster CPUs, an increased number of CPUs, and an increased number of cores in each CPU. Collectively, these trends are making it increasingly more economical to boost the execution parallelization to take advantage of the increased computing power. In this chapter, we look at executing loops in parallel, which is one of the easiest ways to take advantage of the increased computing capability. Much of the chapter consists of Beginner and Advanced Topic blocks.

| Canceling a PLINQ Query | 2. Running LINQ Queries in Parallel | Iterating in Parallel | 1. Executing Loop Iterations in Parallel | Canceling a Parallel Loop |

Consider the for statement and associated code shown in Listing 21.1 and the corresponding results in Output 21.1. The listing calls a method for calculating a section of the decimal expansion of pi, where the parameters are the number of digits and the digit to start. The actual calculation is not germane to the discussion. What is interesting about this calculation is that it is vastly parallelizable; that is, it is remarkably easy to split up a large task—say, computing 1 million decimal digits of pi—into any desired number of smaller tasks that can all be in

1021
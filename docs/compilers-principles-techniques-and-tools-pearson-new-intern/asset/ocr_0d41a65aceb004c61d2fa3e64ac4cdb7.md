program model we used for data-flow analysis in Chapter 9 is inadequate for parallelization and locality optimization. The reason is that work on data-flow analysis assumes we don’t distinguish among the ways a given statement is reached, and in fact these Chapter 9 techniques take advantage of the fact that we don’t distinguish among different executions of the same statement, e.g., in a loop. To parallelize a code, we need to reason about the dependencies among different dynamic executions of the same statement to determine if they can be executed on different processors simultaneously.

This chapter focuses on techniques for optimizing the class of numerical applications that use arrays as data structures and access them with simple regular patterns. More specifically, we study programs that have affine array accesses with respect to surrounding loop indexes. For example, if i and j are the index variables of surrounding loops, then Z[i][j] and Z[i][i + j] are affine accesses. A function of one or more variables, x₁, x₂, …, xₙ is affine if it can be expressed as a sum of a constant, plus constant multiples of the variables, i.e., c₀ + c₁x₁ + c₂x₂ + ··· + cₙxₙ, where c₀, c₁, …, cₙ are constants. Affine functions are usually known as linear functions, although strictly speaking, linear functions do not have the c₀ term.

Here is a simple example of a loop in this domain:

```
```c
for (i = 0; i < 10; i++) {
    Z[i] = 0;
}
```
```

Because iterations of the loop write to different locations, different processors can execute different iterations concurrently. On the other hand, if there is another statement Z[j] = 1 being executed, we need to worry about whether i could ever be the same as j, and if so, in which order do we execute those instances of the two statements that share a common value of the array index.

Knowing which iterations can refer to the same memory location is important. This knowledge lets us specify the data dependences that must be honored when scheduling code for both uniprocessors and multiprocessors. Our objective is to find a schedule that honors all the data dependences such that operations that access the same location and cache lines are performed close together if possible, and on the same processor in the case of multiprocessors.

The theory we present in this chapter is grounded in linear algebra and integer programming techniques. We model iterations in an n-deep loop nest as an n-dimensional polyhedron, whose boundaries are specified by the bounds of the loops in the code. Affine functions map each iteration to the array locations it accesses. We can use integer linear programming to determine if there exist two iterations that can refer to the same location.

The set of code transformations we discuss here fall into two categories: affine partitioning and blocking. Affine partitioning splits up the polyhedra of iterations into components, to be executed either on different machines or one-by-one sequentially. On the other hand, blocking creates a hierarchy of iterations. Suppose we are given a loop that sweeps through an array row-by-
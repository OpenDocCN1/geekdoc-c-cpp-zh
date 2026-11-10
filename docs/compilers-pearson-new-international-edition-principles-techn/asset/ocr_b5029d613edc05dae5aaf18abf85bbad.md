**Exercise 9.8.2:** Consider the inner loop of Fig. 9.10, consisting of blocks B₃ and B₄. If it requires the number of times around the loop, and f is the transfer function for the loop body (i.e., excluding the edge from B₄ to B₃) from the entry of the loop (i.e., the beginning of B₃) to the exit from B₄, then what is fⁱ? Remember that f takes as argument a map m, and m assigns a value to each of variables a, b, d, and e. We denote these values m(a), and so on, although we do not know their true values.

**Exercise 9.8.3:** Now consider the outer loop of Fig. 9.10, consisting of blocks B₂, B₃, B₄, and B₅. Let g be the transfer function for the loop body, from the entry of the loop at B₂ to its exit at B₅. Let i measure the number of iterations of the inner loop of B₃ and B₄ (which count of iterations we cannot know), and let j measure the number of iterations of the outer loop (which we also cannot know). What is gʲ?

# ## 9.9  Summary of Chapter 9

+   - **Global Common Subexpressions:** An important optimization is finding computations of the same expression in two different basic blocks. If one precedes the other, we can store the result the first time it is computed and use the stored result on subsequent occurrences.

+   - **Copy Propagation:** A copy statement, *a = v*, assigns one variable *v* to another, *u*. In some circumstances, we can replace all uses of *v* by *u*, thus eliminating both the assignment and *u*.

+   - **Code Motion:** Another optimization is to move a computation outside the loop in which it appears. This change is only correct if the computation produces the same value each time around the loop.

+   - **Induction Variables:** Many loops have induction variables, variables that take on a linear sequence of values each time around the loop. Some of these are used only to count iterations, and they often can be eliminated, thus reducing the time it takes to go around the loop.

+   - **Data-Flow Analysis:** A data-flow analysis schema defines a value at each point in the program. Statements of the program have associated transfer functions that relate the value before the statement to the value after. Statements with more than one predecessor must have their value defined by combining the values at the predecessors, using a meet (or confluence) operator.

+   - **Data-Flow Analysis on Basic Blocks:** Because the propagation of data-flow values within a block is usually quite simple, data-flow equations are generally set up to have two variables for each block, called IN and OUT, that represent the data-flow values at the beginning and end of the
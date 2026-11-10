
## 9.5. Partial-Redundancy Elimination

![](img/2a44b9071782fade81f3050c3b718341_644_0.png)

Figure 9.30: Examples of (a) global common subexpression, (b) loop-invariant code motion, (c) partial-redundancy elimination.

### Global Common Subexpressions

In Fig. 9.30(a), the expression *b + c* computed in block *B₄* is redundant; it has already been evaluated by the time the flow of control reaches *B₄* regardless of the path taken to get there. As we observe in this example, the value of the expression may be different on different paths. We can optimize the code by storing the result of the computations of *b + c* in blocks *B₂* and *B₃* in the same temporary variable, say *t*, and then assigning the value of *t* to the variable *e* in block *B₄*, instead of reevaluating the expression. Had there been an assignment to either *b* or *c* after the last computation of *b + c* but before block *B₄*, the expression in block *B₄* would not be redundant.

Formally, we say that an expression *b + c* is (fully) redundant at point *p*, if it is an available expression, in the sense of Section 9.2.6, at that point. That is, the expression *b + c* has been computed along all paths reaching point *p*, and the variables *b* and *c* were not redefined after the last expression was evaluated. The latter condition is necessary, because even though the expression *b + c* is textually executed before reaching the point *p*, the value of *b + c* computed at point *p* would have been different, because the operands might have changed.

### Finding “Deep” Common Subexpressions

Using available-expressions analysis to identify redundant expressions only works for expressions that are textually identical. For example, an application of common-subexpression elimination will recognize that t1 in the code fragment

```text
t1 = b + c; a = t1 + d;
```

has the same value as does t2 in

```text
t2 = b + c; e = t2 + d;
```

as long as the variables b and c have not been redefined in between. It does not, however, recognize that a and e are also the same. It is possible to find such “deep” common subexpressions by re-applying common subexpression elimination until no new common subexpressions are found on one round. It is also possible to use the framework of Exercise 9.4.2 to catch deep common subexpressions.

### Loop-Invariant Expressions

Fig. 9.30(b) shows an example of a loop-invariant expression. The expression b + c is loop invariant assuming neither the variable b nor c is redefined within the loop. We can optimize the program by replacing all the re-executions in a loop by a single calculation outside the loop. We assign the computation to a temporary variable, say t, and then replace the expression in the loop by t. There is one more point we need to consider when performing “code motion” optimizations such as this. We should not execute any instruction that would not have executed without the optimization. For example, if it is possible to exit the loop without executing the loop-invariant instruction at all, then we should not move the instruction out of the loop. There are two reasons.

- 1. If the instruction raises an exception, then executing it may throw an exception that would not have happened in the original program.
- 2. When the loop exits early, the “optimized” program takes more time than the original program.

To ensure that loop-invariant expressions in while-loops can be optimized, compilers typically represent the statement

```text
while c {
    S;
}
```

in the same way as the statement

```text
if c {
    repeat
        S;
    until not c;
}
```

In this way, loop-invariant expressions can be placed just prior to the repeat-until construct.

Unlike common-subexpression elimination, where a redundant expression computation is simply dropped, loop-invariant-expression elimination requires an expression from inside the loop to move outside the loop. Thus, this optimization is generally known as “loop-invariant code motion.” Loop-invariant code motion may need to be repeated, because once a variable is determined to have a loop-invariant value, expressions using that variable may also become loop-invariant.

### Partially Redundant Expressions

An example of a partially redundant expression is shown in Fig. 9.30(c). The expression *b + c* in block *B₄* is redundant on the path *B₁ → B₂ → B₄*, but not on the path *B₁ → B₃ → B₄*. We can eliminate the redundancy on the former path by placing a computation of *b + c* in block *B₃*. All the results of *b + c* are written into a temporary variable, *t*, and the calculation in block *B₄* is replaced with *t*. Thus, like loop-invariant code motion, partial-redundancy elimination requires the placement of new expression computations.

### 9.5.2 Can All Redundancy Be Eliminated?

Is it possible to eliminate all redundant computations along every path? The answer is “no,” unless we are allowed to change the flow graph by creating new blocks.

**Example 9.28:** In the example shown in Fig. 9.31(a), the expression of *b + c* is computed redundantly in block *B₄* if the program follows the execution path *B₁ → B₂ → B₄*. However, we cannot simply move the computation of *b + c* to block *B₃*, because doing so would create an extra computation of *b + c* when the path *B₁ → B₃ → B₅* is taken.

What we would like to do is to insert the computation of *b + c* only along the edge from block *B₃* to block *B₄*. We can do so by placing the instruction in a new block, say, *B₆*, and making the flow of control from *B₃* go through *B₆* before it reaches *B₄*. The transformation is shown in Fig. 9.31(b).

![](img/2a44b9071782fade81f3050c3b718341_647_0.png)

Figure 9.31: B₃ → B₄ is a critical edge.

We define a *critical edge* of a flow graph to be any edge leading from a node with more than one successor to a node with more than one predecessor. By introducing new blocks along critical edges, we can always find a block to accommodate the desired expression placement. For instance, the edge from B₃ to B₄ in Fig. 9.31(a) is critical, because B₃ has two successors, and B₄ has two predecessors.

Adding blocks may not be sufficient to allow the elimination of all redundant computations. As shown in Example 9.29, we may need to duplicate code so as to isolate the path where redundancy is found.

**Example 9.29:** In the example shown in Figure 9.32(a), the expression of *b + c* is computed redundantly along the path B₁ → B₂ → B₄ → B₆. We would like to remove the redundant computation of *b + c* from block B₆ in this path and compute the expression only along the path B₁ → B₃ → B₄ → B₆. However, there is no single pre-point or edge in the source program that corresponds uniquely to the latter path. To create such a program point, we can duplicate the pair of blocks B₄ and B₆, with one pair reached through B₂ and the other reached through B₃, as shown in Figure 9.32(b). The result of *b + c* is saved in variable *t* in block B₂, and moved to variable *d* in B₆′, the copy of B₆ reached from B₂. □

Since the number of paths is exponential in the number of conditional branches in the program, eliminating all redundant expressions can greatly increase the size of the optimized code. We therefore restrict our discussion of redundancy-elimination techniques to those that may introduce additional blocks but that do not duplicate portions of the control flow graph.

![](img/2a44b9071782fade81f3050c3b718341_648_0.png)

Figure 9.32: Code duplication to eliminate redundancies.

### 9.5.3 The Lazy-Code-Motion Problem

It is desirable for programs optimized with a partial-redundancy-elimination algorithm to have the following properties:

- 1. All redundant computations of expressions that can be eliminated without code duplication are eliminated.
- 2. The optimized program does not perform any computation that is not in the original program.
- 3. Expressions are computed at the latest possible time.

The last property is important because the values of expressions found to be redundant are usually held in registers until they are used. Computing a value as late as possible minimizes its lifetime — the duration between the time the value is defined and the time it is last used, which in turn minimizes its usage of a register. We refer to the optimization of eliminating partial redundancy with the goal of delaying the computations as much as possible as *lazy code motion*.

To build up our intuition of the problem, we first discuss how to reason about partial redundancy of a single expression along a single path. For convenience, we assume for the rest of the discussion that every statement is a basic block of its own.

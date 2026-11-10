
## 8.5 Optimization of Basic Blocks

We can often obtain a substantial improvement in the running time of code merely by performing *local* optimization within each basic block by itself. More thorough *global* optimization, which looks at how information flows among the basic blocks of a program, is covered in later chapters, starting with Chapter 9. It is a complex subject, with many different techniques to consider.

### 8.5.1 The DAG Representation of Basic Blocks

Many important techniques for local optimization begin by transforming a basic block into a DAG (directed acyclic graph). In Section 6.1.1, we introduced the DAG as a representation for single expressions. The idea extends naturally to the collection of expressions that are created within one basic block. We construct a DAG for a basic block as follows:

- 1. There is a node in the DAG for each of the initial values of the variables appearing in the basic block.
- 2. There is a node *N* associated with each statement *s* within the block. The children of *N* are those nodes corresponding to statements that are the last definitions, prior to *s*, of the operands used by *s*.
- 3. Node *N* is labeled by the operator applied at *s*, and also attached to *N* is the list of variables for which it is the last definition within the block.
- 4. Certain nodes are designated *output nodes*. These are the nodes whose variables are *live on exit* from the block; that is, their values may be used later, in another block of the flow graph. Calculation of these “live variables” is a matter for global flow analysis, discussed in Section 9.2.5.

The DAG representation of a basic block lets us perform several code-improving transformations on the code represented by the block.

- a) We can eliminate *local common subexpressions*, that is, instructions that compute a value that has already been computed.
- b) We can eliminate *dead code*, that is, instructions that compute a value that is never used.
- c) We can reorder statements that do not depend on one another; such reordering may reduce the time a temporary value needs to be preserved in a register.
- d) We can apply algebraic laws to reorder operands of three-address instructions, and sometimes thereby simplify the computation.

### 8.5.2 Finding Local Common Subexpressions

Common subexpressions can be detected by noticing, as a new node M is about to be added, whether there is an existing node N with the same children, in the same order, and with the same operator. If so, N computes the same value as M and may be used in its place. This technique was introduced as the “value-number” method of detecting common subexpressions in Section 6.1.1.

**Example 8.10:** A DAG for the block

```
a = b + c
b = a - d
c = b + c
d = a - d
```

is shown in Fig. 8.12. When we construct the node for the third statement c = b + c, we know that the use of b in b + c refers to the node of Fig. 8.12 labeled −, because that is the most recent definition of b. Thus, we do not confuse the values computed at statements one and two.

![](img/a29d16e454785bb105e96ef448ac07f6_538_0.png)

Figure 8.12: DAG for basic block in Example 8.10

However, the node corresponding to the fourth statement d = a − d has the operator − and the nodes with attached variables a and d as children. Since the operator and the children are the same as those for the node corresponding to statement two, we do not create this node, but add d to the list of definitions for the node labeled −. □

It might appear that, since there are only three nonleaf nodes in the DAG of Fig. 8.12, the basic block in Example 8.10 can be replaced by a block with only three statements. In fact, if b is not live on exit from the block, then we do not need to compute that variable, and can use d to receive the value represented by the node labeled − in Fig. 8.12. The block then becomes

```
a = b + c
d = a - d
c = d + c
```

However, if both b and d are live on exit, then a fourth statement must be used to copy the value from one to the other.¹

**Example 8.11:** When we look for common subexpressions, we really are looking for expressions that are guaranteed to compute the same value, no matter how that value is computed. Thus, the DAG method will miss the fact that the expression computed by the first and fourth statements in the sequence

```
a = b + c
b = b - d
c = c + d
e = b + c
```

is the same, namely b₀ + c₀. That is, even though b and c both change between the first and last statements, their sums remain the same, because b + c = (b − d) + (c + d). The DAG for this sequence is shown in Fig. 8.13, but does not exhibit any common subexpressions. However, algebraic identities applied to the DAG, as discussed in Section 8.5.4, may expose the equivalence. □

![](img/a29d16e454785bb105e96ef448ac07f6_539_0.png)

Figure 8.13: DAG for basic block in Example 8.11

### 8.5.3 Dead Code Elimination

The operation on DAGs that corresponds to dead-code elimination can be implemented as follows. We delete from a DAG any root (node with no ancestors) that has no live variables attached. Repeated application of this transformation will remove all nodes from the DAG that correspond to dead code.

**Example 8.12:** If, in Fig. 8.13, a and b are live but c and e are not, we can immediately remove the root labeled e. Then, the node labeled c becomes a root and can be removed. The roots labeled a and b remain, since they each have live variables attached. □

¹ In general, we must be careful, when reconstructing code from DAGs, how we choose the names of variables. If a variable x is defined twice, or if it is assigned once and the initial value x₀ is also used, then we must make sure that we do not change the value of x until we have made all uses of the node whose value x previously held.

```
a = b + c
t = c + d
e = t + b
```

If t is not needed outside this block, we can change this sequence to

```
a = b + c
e = a + d
```

using both the associativity and commutativity of +.

The compiler writer should examine the language reference manual carefully to determine what rearrangements of computations are permitted, since (because of possible overflows or underflows) computer arithmetic does not always obey the algebraic identities of mathematics. For example, the Fortran standard states that a compiler may evaluate any mathematically equivalent expression, provided that the integrity of parentheses is not violated. Thus, a compiler may evaluate x * y − x * z as x * (y − z), but it may not evaluate a + (b − c) as (a + b) − c. A Fortran compiler must therefore keep track of where parentheses were present in the source language expressions if it is to optimize programs in accordance with the language definition.

### 8.5.5 Representation of Array References

At first glance, it might appear that the array-indexing instructions can be treated like any other operator. Consider for instance the sequence of three-address statements:

```
x = a[i]
a[j] = y
z = a[i]
```

If we think of a[i] as an operation involving a and i, similar to a + i, then it might appear as if the two uses of a[i] were a common subexpression. In that case, we might be tempted to “optimize” by replacing the third instruction z = a[i] by the simpler z = x. However, since j could equal i, the middle statement may in fact change the value of a[i]; thus, it is not legal to make this change.

The proper way to represent array accesses in a DAG is as follows.

- 1. An assignment from an array, like x = a[i], is represented by creating a node with operator =[] and two children representing the initial value of the array, a₀ in this case, and the index i. Variable x becomes a label of this new node.
- 2. An assignment to an array, like a[j] = y, is represented by a new node with operator []= and three children representing a₀, j, and y. There is no variable labeling this node. What is different is that the creation of


Now, since we need both registers for the left child of the root, we need to generate the instruction

```
ST  t3, R2
```

Next, the left child of the root is handled. Again, the number of registers is sufficient for this child, and the code is

```
LD  R2, b
LD  R1, a
SUB R2, R1, R2
```

Finally, we reload the temporary that holds the right child of the root with the instruction

```
LD  R1, t3
```

and execute the operation at the root of the tree with the instruction

```
ADD R2, R2, R1
```

The complete sequence of instructions is shown in Fig. 8.25.

```
LD  R2, d
LD  R1, c
ADD R2, R1, R2
LD  R1, e
MUL R2, R1, R2
ST  t3, R2
LD  R2, b
LD  R1, a
SUB R2, R1, R2
LD  R1, t3
ADD R2, R2, R1
```

Figure 8.25: Optimal three-register code for the tree of Fig. 8.23, using only two registers

### 8.10.4 Exercises for Section 8.10

**Exercise 8.10.1:** Compute Ershov numbers for the following expressions:

- a) $a/(b+c)-d*(e+f)$.
- b) $a+b*(c*(d+e))$.
- c) \((-a + *p) * ((b - *q)/(−c + *r))\).

**Exercise 8.10.2:** Generate optimal code using two registers for each of the expressions of Exercise 8.10.1.

**Exercise 8.10.3:** Generate optimal code using three registers for each of the expressions of Exercise 8.10.1.

**Exercise 8.10.4:** Generalize the computation of Ershov numbers to expression trees with interior nodes with three or more children.

**Exercise 8.10.5:** An assignment to an array element, such as `a[i] = x`, appears to be an operator with three operands: `a`, `i`, and `x`. How would you modify the tree-labeling scheme to generate optimal code for this machine model?

**Exercise 8.10.6:** The original Ershov numbers were used for a machine that allowed the right operand of an expression to be in memory, rather than a register. How would you modify the tree-labeling scheme to generate optimal code for this machine model?

**Exercise 8.10.7:** Some machines require two registers for certain single-precision values. Suppose that the result of a multiplication of single-register quantities requires two consecutive registers, and when we divide `a/b`, the value of `a` must be held in two consecutive registers. How would you modify the tree-labeling scheme to generate optimal code for this machine model?

## 8.11 Dynamic Programming Code-Generation

Algorithm 8.26 in Section 8.10 produces optimal code from an expression tree using an amount of time that is a linear function of the size of the tree. This procedure works for machines in which all computation is done in registers and in which instructions consist of an operator applied to two registers or to a register and a memory location.

An algorithm based on the principle of dynamic programming can be used to extend the class of machines for which optimal code can be generated from expression trees in linear time. The dynamic programming algorithm applies to a broad class of register machines with complex instruction sets.

The dynamic programming algorithm can be used to generate code for any machine with \(r\) interchangeable registers \(R_0, R_1, \ldots, R_{r-1}\) and load, store, and operation instructions. For simplicity, we assume every instruction costs one unit, although the dynamic programming algorithm can easily be modified to work even if each instruction has its own cost.

### 8.11.1 Contiguous Evaluation

The dynamic programming algorithm partitions the problem of generating optimal code for an expression into the subproblems of generating optimal code for the subexpressions of the given expression. As a simple example, consider an expression $E$ of the form $E_1 + E_2$. An optimal program for $E$ is formed by combining optimal programs for $E_1$ and $E_2$, in one or the other order, followed by code to evaluate the operator +. The subproblems of generating optimal code for $E_1$ and $E_2$ are solved similarly.

An optimal program produced by the dynamic programming algorithm has an important property. It evaluates an expression $E = E_1\ \mathbf{op}\ E_2$ “contiguously.” We can appreciate what this means by looking at the syntax tree $T$ for $E$:

![](img/2a44b9071782fade81f3050c3b718341_578_0.png)

Here $T_1$ and $T_2$ are trees for $E_1$ and $E_2$, respectively.

We say a program $P$ evaluates a tree $T$ contiguously if it first evaluates those subtrees of $T$ that need to be computed into memory. Then, it evaluates the remainder of $T$ either in the order $T_1$, $T_2$, and then the root, or in the order $T_2$, $T_1$, and then the root, in either case using the previously computed values from memory whenever necessary. As an example of noncontiguous evaluation, $P$ might first evaluate part of $T_1$ leaving the value in a register (instead of memory), next evaluate $T_2$, and then return to evaluate the rest of $T_1$.

For the register machine in this section, we can prove that given any machine-language program $P$ to evaluate an expression tree $T$, we can find an equivalent program $P'$ such that

- 1. $P'$ is of no higher cost than $P$,
- 2. $P'$ uses no more registers than $P$, and
- 3. $P'$ evaluates the tree contiguously.

This result implies that every expression tree can be evaluated optimally by a contiguous program.

By way of contrast, machines with even-odd register pairs do not always have optimal contiguous evaluations; the x86 architecture uses register pairs for multiplication and division. For such machines, we can give examples of expression trees in which an optimal machine language program must first evaluate into a register a portion of the left subtree of the root, then a portion of the right subtree, then another part of the left subtree, then another part of the right, and so on. This type of oscillation is unnecessary for an optimal evaluation of any expression tree using the machine in this section.

of i. The smallest cost in the vector for the root of $T$ gives the minimum cost of evaluating $T$.

**Example 8.28:** Consider a machine having two registers R0 and R1, and the following instructions, each of unit cost:

```
LD  Ri, Mj       // Ri = Mj
op  Ri, Ri, Rj    // Ri = Ri op Rj
op  Ri, Ri, Mj    // Ri = Ri op Mj
LD  Ri, Rj       // Ri = Rj
ST  Mi, Rj       // Mi = Rj
```

In these instructions, $R_i$ is either R0 or R1, and $M_j$ is a memory location. The operator $op$ represents any arithmetic operator.

Let us apply the dynamic programming algorithm to generate optimal code for the syntax tree in Fig. 8.26. In the first phase, we compute the cost vectors shown at each node. To illustrate this cost computation, consider the cost vector at the leaf $a$. $C[0]$, the cost of computing $a$ into memory, is 0 since it is already there. $C[1]$, the cost of computing $a$ into a register, is 1 since we can load it into a register with the instruction LD R0, a. $C[2]$, the cost of loading $a$ into a register with two registers available, is the same as that with one register available. The cost vector at leaf $a$ is therefore (0, 1, 1).

![](img/2a44b9071782fade81f3050c3b718341_580_0.png)

Figure 8.26: Syntax tree for $(a-b)+c*(d/e)$ with cost vector at each node

Consider the cost vector at the root. We first determine the minimum cost of computing the root with one and two registers available. The machine instruction ADD R0, R0, M matches the root, because the root is labeled with the operator +. Using this instruction, the minimum cost of evaluating the root with one register available is the minimum cost of computing its right subtree into memory, plus the minimum cost of computing its left subtree into the register, plus 1 for the instruction. No other way exists. The cost vectors at the right and left children of the root show that the minimum cost of computing the root with one register available is $5+2+1=8$.

Now consider the minimum cost of evaluating the root with two registers available. Three cases arise depending on which instruction is used to compute the root and in what order the left and right subtrees of the root are evaluated.

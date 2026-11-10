```
    LD  R3, d
    LD  R2, c
    ADD R3, R2, R3
```

Next, we generate code for the left child of the right child of the root; this node is the leaf labeled c. Since b = 2, the proper instruction is

```
    LD  R2, e
```

Now we can complete the code for the right child of the root by adding the instruction

```
    MUL R3, R2, R3
```

The algorithm proceeds to generate code for the left child of the root, leaving the result in R3, and with base 1. The complete sequence of instructions is shown in Fig. 8.24. □

```
    LD  R3, d
    LD  R2, c
    ADD R3, R2, R3
    LD  R2, e
    MUL R3, R2, R3
    LD  R2, b
    LD  R1, a
    SUB R2, R1, R2
    ADD R3, R2, R3
```

Figure 8.24: Optimal three-register code for the tree of Fig. 8.23

# ### 8.10.3 Evaluating Expressions with an Insufficient Supply of Registers

When there are fewer registers available than the label of the root of the tree, we cannot apply Algorithm 8.24 directly. We need to introduce some store instructions that spill values of subtrees into memory, and we then need to load those values back into registers as needed. Here is the modified algorithm that takes into account a limitation on the number of registers.

**Algorithm 8.26:** Generating code from a labeled expression tree.

**INPUT:** A labeled tree with each operand appearing once (i.e., no common subexpressions) and a number of registers r ≥ 2.

**OUTPUT:** An optimal sequence of machine instructions to evaluate the root into a register, using no more than r registers, which we assume are R₁, R₂, …, Rᵣ.
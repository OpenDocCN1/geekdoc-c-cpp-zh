# ## 9.2. INTRODUCTION TO DATA-FLOW ANALYSIS

Thus, like a statement, a basic block also generates a set of definitions and kills a set of definitions. The *gen* set contains all the definitions inside the block that are “visible” immediately after the block — we refer to them as *downwards exposed*. A definition is downwards exposed in a basic block only if it is not “killed” by a subsequent definition to the same variable inside the same basic block. A basic block’s *kill* set is simply the union of all the definitions killed by the individual statements. Notice that a definition may appear in both the *gen* and *kill* set of a basic block. If so, the fact that it is in *gen* takes precedence, because in *gen-kill* form, the *kill* set is applied before the *gen* set.

**Example 9.10:** The *gen* set for the basic block

```
```
d1: a = 3
d2: a = 4
```
```

is {*d*₁} since *d*₁ is not downwards exposed. The *kill* set contains both *d*₁ and *d*₂, since *d*₁ kills *d*₂ and vice versa. Nonetheless, since the subtraction of the *kill* set precedes the union operation with the *gen* set, the result of the transfer function for this block always includes definition *d*₂. □

# ### Control-Flow Equations

Next, we consider the set of constraints derived from the control flow between basic blocks. Since a definition reaches a program point as long as there exists at least one path along which the definition reaches, OUT[P] ⊆ IN[B] whenever there is a control-flow edge from P to B. However, since a definition cannot reach a point unless there is a path along which it reaches, IN[B] needs to be no larger than the union of the reaching definitions of all the predecessor blocks. That is, it is safe to assume

```
```
IN[B] = ⋃_{P a predecessor of B} OUT[P]
```
```

We refer to union as the *meet operator* for reaching definitions. In any data-flow schema, the meet operator is the one we use to create a summary of the contributions from different paths at the confluence of those paths.

# ### Iterative Algorithm for Reaching Definitions

We assume that every control-flow graph has two empty basic blocks, an ENTRY node, which represents the starting point of the graph, and an EXIT node to which all exits out of the graph go. Since no definitions reach the beginning of the graph, the transfer function for the ENTRY block is a simple constant function that returns ∅ as an answer. That is, OUT[ENTRY] = ∅.

The reaching definitions problem is defined by the following equations:

```
```
OUT[ENTRY] = ∅
```
```
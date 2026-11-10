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

# 8.5.5 Representation of Array References

At first glance, it might appear that the array-indexing instructions can be treated like any other operator. Consider for instance the sequence of three-address statements:

```
x = a[i]
a[j] = y
z = a[i]
```

If we think of a[i] as an operation involving a and i, similar to a + i, then it might appear as if the two uses of a[i] were a common subexpression. In that case, we might be tempted to “optimize” by replacing the third instruction z = a[i] by the simpler z = x. However, since j could equal i, the middle statement may in fact change the value of a[i]; thus, it is not legal to make this change.

The proper way to represent array accesses in a DAG is as follows.

+   1. An assignment from an array, like x = a[i], is represented by creating a node with operator =[] and two children representing the initial value of the array, a₀ in this case, and the index i. Variable x becomes a label of this new node.
+   
+   2. An assignment to an array, like a[j] = y, is represented by a new node with operator []= and three children representing a₀, j, and y. There is no variable labeling this node. What is different is that the creation of
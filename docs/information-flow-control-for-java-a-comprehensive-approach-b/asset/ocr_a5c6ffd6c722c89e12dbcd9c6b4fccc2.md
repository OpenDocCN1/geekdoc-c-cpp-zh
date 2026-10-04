# CHAPTER 2 DEPENDENCE GRAPHS AND SLICING FOR
OBJECT-ORIENTED LANGUAGES

elements $L$ in $\mathcal{L} = (L, \le, \varnothing, D, \cup, \cap)$. The transfer functions are derived from
t abstract semantics of variable assignment:

```
$F_n(X) = X \setminus kill(n) \cup gen(n)$
```

A statement defines the variables in $Def(n)$, so all definitions in $D$ that define
the same variables can no longer be visible after $n$ has executed, i.e. they are
overwritten or "killed" by this definition. All elements of $Def(n)$ are "generated"
by that statement and thus visible after its execution. This can formalized

```
$gen(n) := Def(n)$
```

```
$kill(n) := \bigcup_{v \in Def(n)} D_v, \text{ where } D_v := \{d \in D \mid v = var(d)\}$
```

As reaching definitions is distributive monotone dataflow framework,
work MOP computed by Kiddall's algorithm with which the MOP solution
coincides.

# 2.1.3 Static Assignment Form

A very popular representation is called *static single-assignment (SSA)*
form [CFR*91]. It separates several values from the program's
variables and thus enables several more effective optimizations. A program
is in static single-assignment form if every variable is assigned at most once
t the source code. It is called *static* because the variable may well be
assigned to multiple times during program execution, e.g. in a loop.
the outstanding power of SSA form is that it makes def-use,
asasputed by reaching definitions in the last section, explicit and allows-
sensitive analysis for the program's variables, as each variable is assigned to
exactly once. Because of this SSA form becomes a standard intermediate
representation in program analysis.

To compute the static single-assignment form [CFR*91], usually
troduces a subscript for each variable that is incremented at each assignment
statement. At points in the control flow graph, new assignments with a
$\phi$-operator need to be inserted to represent the choice of the ap-\proprietary variable according to the program's flow. Note that programs in SSA
form are equivalent to the original program. As example, consider Figure 2.2,
where a program is deployed alongside its SSA form. In line 5 of the SSA form,
$sum2$ is defined as $sum1$, if the loop has not yet been entered, or
el as $sum3$, the last value defined in the loop body.

# 2.2 Program Slicing

A slice contains only those statements of a program potentially
influence the execution of a given statement. The idea of (static)
program slicing was first presented by Weiser [Wei79,Wei81,Wei84] in 1979.
Weiser formulated the seminal idea that, while debugging, programmers build
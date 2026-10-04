
# 5.4. DYNAMIC PATH CONDITIONS IN DEPENDENCE GRAPHS

## 5.4.3 Dynamic Path Conditions

### Refinement by Dynamic Chopping

When constructing a path condition from a statement to another, all paths between these two statements are determined with a chop in the static dependence graph. As mentioned in Section 5.2.1, the accuracy of the path condition for the executed program can be increased if a dynamic chop is used instead. The dynamic dependence graph usually contains only the edges that actually place and thus this dynamic chop will yield a much smaller number of paths between these two statements.

As an example, consider Figure 1. If the execution trace is 1,2,3,4,7,9 then the chop between 2 and 9 is 2,3,4,7,9. Statement 5 is never executed in this setting and thus be removed from the dynamic chop. A static chop would conservatively have to add it. With the dynamic chop one omits the paths 2,3,4,5,7,9 and 2,3,4,5,7,9 in the path condition between 2 and 9.

Although our path condition generator reuses partial information and thus half the number of paths does not yield 50% shorter path condition, this example also shows the impact of this refinement.

### Refinement by Traced Values

In order to strengthen a given path condition PC with runtime information, the trace is analyzed to retrieve the variable assignments. As the analyzed program went through a series of assignments during runtime, all of them have to be captured in a restrictive clause R. This clause, in turn, can be used to make path conditions stronger.

First, the intersection V of variables used in the path condition PC and the trace T is determined:

```
V = {v | v \in var(T) \intercap var(PC)}
```

For each variable $v$ the values it carried during the trace are extracted, let $\beta(v)$ be the set of $w_i$ that $v$ has constrained:

```
\beta(v) = (v = w_i) \vee (v = w_j) \vee \dots$
```

Now the restrictive clause R can be described as the conjunction of all value sets:

```
R = \bigwedge_{v_i \in V} \beta(v_i)
```

In order to make the path condition PC stronger, the results from Section 5.2.1 are used and both clauses are conjunctively combined

```
PC' = PC \wedge R
```

yielding the stronger and thus more precise path condition PC'.

Because of the SSA-like form, variables only match if their index numbers are the same, so that multiple assignments are handled. This makes mandatory

for the program trace to list variables with their respective node numbers as in Figure 5.10 which shows a simple trace for a run of the program from Figure 5.2.

Note that the node numbers are different to the SSA-numbers from Figure 5.2 and thus, the path condition for a flow from line 1 to 5 is PC(1,5) = (x_3 < 7) \wedge (x_7 = 8). For this path condition the trace yields the variable assignments

```
$R = (x_3 = 2 \vee x_3 = 4 \vee x_3 = 6) \wedge (x_7 = 4 \vee x_7 = 6) \vee (x_7 = 8)$
```

Again, both clauses are conjunctively combined to $PC' = PC \wedge R$ yielding the stronger and more precise path condition $PC'$.

```
$PC' = (x_3 = 2 \vee x_3 = 4 \vee x_3 = 6) \wedge (x_7 = 8)$
```

# CHAPTER 5. PATH CONDITIONS

```
1 LINE 1
2 USE a_2 2
3 DEF x_1 2
4 LINE 2
5 USE x_3 2
6 LINE 3
7 USE y_5 2
8 USE x_6 2
9 DEF x_4 4
10 LINE 4
11 USE x_7 2
12 LINE 2
13 USE x_3 4
14 LINE 3
15 USE y_5 2
16 USE x_4 4
17 DEF x_4 6
18 LINE 4
19 USE x_7 6
20 LINE 2
21 USE x_3 6
22 LINE 3
23 USE y_5 2
24 USE x_6 6
25 DEF x_4 8
26 LINE 4
27 USE x_7 8
28 LINE 5
29 USE x_8 8
30 LINE 2
31 USE x_3 8
```

Figure 5.10: A simple program trace along with their respective node numbers as Figure 5.2

# 5.4. DYNAMIC PATH CONDITIONS IN DEPENDENCE GRAPHS

### Correctness of Dynamic Path Conditions

Sometimes only fragments of a trace are available due to a "defective recorder" or intentionally to save memory. While fragmented traces are generally useless for dynamic slicing (see Section 5.4.1), they still hold valuable information for strengthening path conditions.

```
$x = 0 \vee x = 1$$
```

while the variable assignment states actually were

```
$x = 0 \vee x = 2$$
```

The restricted path condition

```
$PC' = (x > 1) \wedge (x = 0 \vee x = 1) \equiv false$$
```

would be in contradiction to the actual program state (x = 2) and then definitely rules out data dependence where it may be possible.

To avoid unsound path conditions, it is conservatively assumed that there is an additional unknown value $\perp$ for each variable representing the assignments which occurred but were not traced due to some memory. This measures yields a correctly restricted path condition as the fragmentation of the trace flows. For our example, the resulting path condition is

```
$$(x > 1) \wedge (x = 0 \vee x = 1 \vee \perp) \\\equiv (x > 1 \wedge x = \perp) \equiv x > 1$$
```

Only if the completeness of the trace (at least certain variables, see Section 5.4.1) can be guaranteed, one may abandon this conservative measure (for those variables).

It may seem using this trick one doesn't gain any additional information of dynamic variable. To show the advantage of variable traces containing unknown values, consider the path PC(1,5) of Figure 5.1. With a fragmented variable forming the restrictive clause (x = 5 \vee x = \perp$) the improved path condition from 1 to 5 will be:

```
$PC(1,5) \equiv (n > 0 \vee n > 0) \wedge (x = 5 \vee x = \perp) \wedge (n = 3 \vee n = \perp)$$$
```

It is immediately clear that the traced variable x = 5 and n = 3 may trigger an influence from line 1 to line 5.

This tiny example shows that while restrictive clauses cannot be used to evaluate a clause of the path condition to false, they may reveal input values that triggered an illegal information flow.

149

# CHAPTER 5. PATH CONDITIONS

## 5.4.4 Related Work

Symbolic execution is a technique that executes a program with symbols instead of concrete values for the parameters. During execution, a predicate Φ (initially true) binds to constrain the values. When a branch is taken, the predicate is updated to reflect the condition for that branch. As it represents the conditions for the current path through the CFG, it is often called *path condition* as well, as it represents the condition for taking a specific path, it is more than an execution condition in our work. Today's systems for symbolic execution are mainly based on theorem provers or model checkers. Theorem prover based systems like in ESC/Java [FLL02] require manual annotations to generate verification conditions, while our approach allows them fully automatically. Other systems rely on model checkers [DRH07] which are semi-automatic but can cope with state explosion. Most symbolic execution systems perform a per-method analysis only, while our approach automatically generates procedural conditions.

Recent work by J has been using path slicing [JM05] as input towards the CFG and eliminates all the operations that are irrelevant towards the target location. The result is a condition for the reachability of the target location, its insufficiency is sufficient for the infeasibility of the path. The technique does not work on the PD but on the CFG only. It has shown effective for elimination of counterexamples provided by the model checker Blast. For our application this approach does not seem beneficial as to check each path on its own, which produces a necessary condition for all paths between two statements and share common subsets.

Parametric slicing [FRT95] allows specification of constraints over the program's input. A returning system generates program slice satisfying these constraints. Conditional program slicing [CCL08] is a similar technique that slices based on a first order logic formula on the input variables. The conditioned slice is on deleting statements while preserving the program's behavior. Both differ from path conditions in that they do not determine input values but take them as input. In contrast, path conditions provide a logic formula that must be satisfied for an information to be feasible. Constraint solvers reduce this condition to input values that satisfy the formula.

Boolean paths as presented in this work and in [Sne96, RS02, Bob05] cannot express temporal properties. For example, they cannot express that it is necessary for a flow loop condition that holds and later it no longer, such that the loop terminates. Boolean conditions become conservative when analyzing loops and conditions that involve loop variables. A recent approach by Lochbiler and Snelting [LS09] extends path conditions with temporal logic to circumvent these imprecisions. Witnesses are created by model checking instead of constraint solvers.

Dynamic Analyses Correctly and efficiently collecting trace data is a nontrivial task. Several solutions have been proposed in literature:

150


## 2.2. PROGRAM SLICING

```
read(n);
i1 = 1;
sum = 0;
prod = 1;
while (i <= n) {
  sum = sum + i;
  prod = prod * i;
  i++;
}
write(sum);
write(prod);
```

Figure 2.2: Example program and SSA form

program abstraction in their minds [Wei82] for which he coined the name program slice. In his definition, a slice is an executable program, with some statements of the original program removed. For a given-slicing criterion $C = (n, V)$, a tuple consisting of a statement and a subset of the program's variables, such reduced program $S$ is called a reduced program slice if it fulfills its properties:

- 1. $S$ must be a valid program, and

- 2. whenever $P$ halts for a given input, $S$ halts for input, computing the same values for the variables in $V$ whenever the statement $n$ is executed.

A formal definition of this idea was presented in [Wei84]. Trivially, every program is a slice of itself. A slice is called statement-minimal for a given criterion, if no other slice for that criterion contains fewer statements. Unfortunately, statement-minimal slices are not unique in general, and their computation is undecidable. Weiser formulated the first algorithm for slicing [Wei84], an iterative dataflow analysis on the source code level.

**Semantics of Slicing** Slice does not preserve traditional program semantics in which the program and its slices are defined [CF89, GM03]. The problem with the standard semantics is that slicing may remove non-terminating portions of a program, i.e. transform a non-terminating program into a terminating one. In this case, the slice clearly has different semantics from the original program. However, a recent, non-standard semantics has been found that is preserved under program slicing. Danicic et al. [DHO07] present a non-strict semantics for a simple while language that is consistent with program slicing.

# CHAPTER 2 DEPENDENCE GRAPHS AND SLICING FOR OBJECT-ORIENTED LANGUAGES

### 2.2.1 Slicing in the PDG

Lateern and Oppenstein [OO84] presented an alternative way of slicing: they reformulate slicing as a reachability analysis in a program representation called Program Dependence Graph (PDG) as defined by Ferrante et al. [FOW87]. In the PDG, slicing can be done in linear time with the number of statements, with a single backward-traversal of dependences between these statements (defined later). In contrast to the executable slices of Weiss's algorithm, the PDG do not necessarily represent executable slices, i.e. the first property of a slice may be violated. The notion of a static slice with a PDG is rather the set of statements which directly or indirectly affect the slicing criterion. Thus the slice may not be syntactically correct, or may be missing, which changes the program semantics. To circumvent these restrictions, several extensions of slicing in PDGs were presented that also execute executable [BH93, CF94, Agr94, HD98, HLB96].

The PDG is defined in terms of the control flow graph: it contains all the nodes of the CFG. Instead, nodes are connected by data and control dependences.

Control dependence exists between two statements, a statement directly controls the execution of the other statement. In structured programs, control dependence is equivalent to the nesting level of source code: Each statement is indented by the enclosing branch or loop point. In the presence of arbitrary control flow, control dependence is defined in terms of post-dominator [FOW87]. A node $x$ in the CFG is post-dominated by $y$ if all paths from $x$ to END pass through $y$. Some definitions exclude the case that a node does postdominate itself.

**Definition 2.8 (Control Dependence).** A node $y$ is control dependent on node $x$ ($x \to y$)

- there exists a path $p$ from $x$ to $y$ in the CFG, such that $y$ post-dominates every node in $p$ (except for $x$).
- $x$ is not post-dominated by $y$

There is always an immediate post-dominator for each statement that has a post-dominator, i.e. a post-dominator that does not dominate another post-dominator of the same statement. This can be depicted as a tree, where only the immediate post-dominator relation is depicted, post-dominance can be found by paths in the tree. As an example Figure 2.3, which shows the post-dominator tree (left) and the corresponding control dependence (sub)graph for the example program in Figure 2.2. For example, node 5 is immediately post-dominated by END. There is a control dependence $5 \to 7$, as 7 can be avoided on the path from 5 to END, and 7 post-dominates all nodes on the path (5, 6, 7) except 5.

> ²If post-dominance is not reflexive, then also for $y$

![](img/27c6595637bae6b27613772d7079f8a2_42_0.png)

Figure 2.3: Post-dominator tree and control dependence subgraph for the example program in 2.2. Edges are implicitly directed downwards.

Definition 2.8 is equivalent to the intuition outlined above for structured programs. Ferrante et al. [FOW87] presented an approach to compute control dependence: They first compute the post-dominator tree with the fast Lengauer-Tarjan algorithm [LLT9]. For every edge $x \to y$ where $y$ is not dominated by $x$, one moves upwards from $y$ in the post-dominator tree. Every node $z$ visited before $x$'s parent is control dependent on $x$. The control dependence edge $x \to z$ is labeled with $l(v,y)$, the label of the control flow edge. To obtain a synthetic control flow edge (with label false, the original edge from START to the first statement is labeled true) is inserted between START and END. Therefore, the START node will be the root in the control dependence subgraph. This synthetic edge is only inserted when computing control dependence and ignored for other analyses.

## Data Dependence

Originally [FOW87], data dependence comprised several types of dependences like flow dependence, output dependence and anti-dependence, but for the purpose of slicing, usually only flow dependence is relevant. For that reason, the term data dependence is used interchangeably with flow dependence in that context. The intuition between a flow dependence $x \xrightarrow{def} y$ is that $x$ computes a value that may be used at node $y$ in some feasible execution. In some cases, a distinction between loop-carried and loop-independent dependences is made. In the sequel, data dependence will stand for loop-carried.

# CHAPTER 2 DEPENDENCE GRAPHS AND SLICING FOR OBJECT-ORIENTED LANGUAGES

```
read(n);
i = 1;
sum = 0;
prod = 1;
while (i <= n) {
  sum = sum + i;
  prod = prod * i;
  i++;
}
write(sum);
write(prod);
```

![](img/27c6595637bae6b27613772d7079f8a2_43_0.png)

**Definition 2.9 (Data Dependence).** Let Ref($x$) denote the set of variables referenced at $x$. Then a node $y$ is dependent on node $x$ ($x \rightarrowrightarrow y$) if

- exists a variable $v$ with $v \in \text{Def}(x)$ and $v \in \text{Ref}(y)$
- exists a path $P$ in the CFG from $x$ to $y$ where the definition of $v$ is not killed (i.e. $x$ is a reaching definition of $y$).

As mentioned, the program dependence graph consists of the nodes of the CFG (sometimes the END node is omitted as it has no- or outgoing edges) with control and data dependence replacing the control flow edges. Consider the program dependence graph of our example in Figure 2.4. The data dependences are depicted in green, control dependencies in blue. Since statement 1 defines a variable that is referenced at line 5 and not overwritten inbetween, there is a data dependence from 1 to 5. The condition in line 5 determines how often the loop is executed, so all the statements in the loop body are connected by control dependence to node 5. Note that dependence graphs may contain loops (see the data dependence at node 6) and multiple edges between two nodes, they are multigraphs.

Data dependence can be computed with reaching definitions analysis directly. But it is explicitly simpler for programs in SSA form, as each variable name is only defined once. Computing DD from SSA form is finding the definition of the referenced variable and if this is defined in a $\Phi$-function building the transitive hull of variables referenced in $\Phi$-functions.

As an example, consider Figure 2.4 again. The definition of $sum_3$ depends on the variable $sum_2$, which is defined in a $\Phi$-function. This function in turn references $sum_1$ and $sum$, none of which is defined in a $\Phi$-function. $sum_3$ is data dependent on itself and on the initialization. This can be seen in Figure 2.4 as data dependences from node 3 to node 6 and from 6 to 6.

## Slicing

The *criterion* for dependence graph based slicing is usually defined different from Weiser's original: Instead of a tuple $(n, V)$, a statement and a set

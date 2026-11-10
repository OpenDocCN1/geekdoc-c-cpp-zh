
![](img/a29d16e454785bb105e96ef448ac07f6_679_0.png)

Figure 9.48: (a) An example flow graph for the reaching definitions problem and (b) its region hierarchy

![](img/a29d16e454785bb105e96ef448ac07f6_680_0.png)

Figure 9.49: Steps in the reduction of the flow graph of Fig. 9.48 to a single region

To summarize the process of decomposing reducible flow graphs hierarchically, we offer the following algorithm.

**Algorithm 9.52:** Constructing a bottom-up order of regions of a reducible flow graph.

**INPUT:** A reducible flow graph *G*.

**OUTPUT:** A list of regions of *G* that can be used in region-based data-flow problems.

**METHOD:**

1. Begin the list with all the leaf regions consisting of single blocks of *G*, in any order.
2. Repeatedly choose a natural loop *L* such that if there are any natural loops contained within *L*, then these loops have had their body and loop regions added to the list already. Add first the region consisting of the body of *L* (i.e., *L* without the back edges to the header of *L*), and then the loop region of *L*.
3. If the entire flow graph is not itself a natural loop, add at the end of the list the region consisting of the entire flow graph.

### 9.7.3 Overview of a Region-Based Analysis

For each region *R*, and for each subregion *R′* within *R*, we compute a transfer function *f*<sub>R,IN[R′]</sub> that summarizes the effect of executing all possible paths leading from the entry of *R* to the entry of *R′*, while staying within *R*.

> **Where “Reducible” Comes From**
>
> We now see why reducible flow graphs were given that name. While we shall not prove this fact, the definition of “reducible flow graph” used in this book, involving the back edges of the graph, is equivalent to several definitions in which we mechanically reduce the flow graph to a single node. The process of collapsing natural loops described in Section 9.7.2 is one of them. Another interesting definition is that the reducible flow graphs are all and only those graphs that can be reduced to a single node by the following two transformations:
>
> - *T₁*: Remove an edge from a node to itself.
> - *T₂*: If node *n* has a single predecessor *m*, and *n* is not the entry of the flow graph, combine *m* and *n*.

We say that a block *B* within *R* is an *exit block* of region *R* if it has an outgoing edge to some block outside *R*. We also compute a transfer function for each exit block *B* of *R*, denoted *f*<sub>R,OUT[B]</sub>, that summarizes the effect of executing all possible paths within *R*, leading from the entry of *R* to the exit of *B*.

We then proceed up the region hierarchy, computing transfer functions for progressively larger regions. We begin with regions that are single blocks, where *f*<sub>B,IN[B]</sub> is just the identity function and *f*<sub>B,OUT[B]</sub> is the transfer function for the block *B* itself. As we move up the hierarchy,

- If *R* is a body region, then the edges belonging to *R* form an acyclic graph on the subregions of *R*. We may proceed to compute the transfer functions in a topological ordering of the subregions.
- If *R* is a loop region, then we only need to account for the effect of the back edges to the header of *R*.

Eventually, we reach the top of the hierarchy and compute the transfer functions for region *R*<sub>n</sub> that is the entire flow graph. How we perform each of these computations will be seen in Algorithm 9.53.

The next step is to compute the data-flow values at the entry and exit of each block. We process the regions in the reverse order, starting with region *R*<sub>n</sub> and working our way down the hierarchy. For each region, we compute the data-flow values at the entry. For region *R*<sub>n</sub>, we apply *f*<sub>Rₙ,IN[R]</sub>(IN[ENTRY]) to get the data-flow values at the entry of the subregions *R* in *R*<sub>n</sub>. We repeat until we reach the basic blocks at the leaves of the region hierarchy.

### 9.7.4 Necessary Assumptions About Transfer Functions

In order for region-based analysis to work, we need to make certain assumptions about properties of the set of transfer functions in the framework. Specifically, we need three primitive operations on transfer functions: composition, meet and closure; only the first is required for data-flow frameworks that use the iterative algorithm.

#### Composition

The transfer function of a sequence of nodes can be derived by composing the functions representing the individual nodes. Let $f_1$ and $f_2$ be transfer functions of nodes $n_1$ and $n_2$. The effect of executing $n_1$ followed by $n_2$ is represented by $f_2 \circ f_1$. Function composition has been discussed in Section 9.2.2, and an example using reaching definitions was shown in Section 9.2.4. To review, let $gen_i$ and $kill_i$ be the $gen$ and $kill$ sets for $f_i$. Then:

$$f_2 \circ f_1(x) = gen_2 \cup ((gen_1 \cup (x - kill_1)) - kill_2)$$

$$\phantom{f_2 \circ f_1(x)} = (gen_2 \cup (gen_1 - kill_2)) \cup (x - (kill_1 \cup kill_2))$$

Thus, the $gen$ and $kill$ sets for $f_2 \circ f_1$ are $gen_2 \cup (gen_1 - kill_2)$ and $kill_1 \cup kill_2$, respectively. The same idea works for any transfer function of the gen-kill form. Other transfer functions may also be composed, but we have to consider each case separately.

#### Meet

Here, the transfer functions themselves are values of a semilattice with a meet operator $\wedge$. The meet of two transfer functions $f_1$ and $f_2$, $f_1 \wedge f_2$, is defined by $(f_1 \wedge f_2)(x) = f_1(x) \wedge f_2(x)$, where $\wedge$ is the meet operator for data-flow values. The meet operator on transfer functions is used to combine the effect of alternative paths of execution with the same end points. Where it is not ambiguous, from now on, we shall refer to the meet operator of transfer functions also as $\wedge$. For the reaching-definitions framework, we have

$$(f_1 \wedge f_2)(x) = f_1(x) \wedge f_2(x)$$

$$\phantom{(f_1 \wedge f_2)(x)} = (gen_1 \cup (x - kill_1)) \cup (gen_2 \cup (x - kill_2))$$

$$\phantom{(f_1 \wedge f_2)(x)} = (gen_1 \cup gen_2) \cup (x - (kill_1 \cap kill_2))$$

That is, the $gen$ and $kill$ sets for $f_1 \wedge f_2$ are $gen_1 \cup gen_2$ and $kill_1 \cap kill_2$, respectively. Again, the same argument applies to any set of gen-kill transfer functions.

#### Closure

If $f$ represents the transfer function of a cycle, then $f^n$ represents the effect of going around the cycle $n$ times. In the case where the number of iterations is not known, we have to assume that the loop may be executed 0 or more times. We represent the transfer function of such a loop by $f^*$, the *closure* of $f$, which is defined by

$$f^* = \bigwedge_{n \ge 0} f^n.$$

Note that $f^0$ must be the identity transfer function, since it represents the effect of going zero times around the loop, i.e., starting at the entry and not moving. If we let $I$ represent the identity transfer function, then we can write

$$f^* = I \wedge \left(\bigwedge_{n>0} f^n\right).$$

Suppose the transfer function $f$ in a reaching definitions framework has a *gen* set and a *kill* set. Then,

$$\begin{aligned}
f^2(x) &= f(f(x)) \\
&= \mathit{gen} \cup ((\mathit{gen} \cup (x - \mathit{kill})) - \mathit{kill}) \\
&= \mathit{gen} \cup (x - \mathit{kill}) \\
f^3(x) &= f(f^2(x)) \\
&= \mathit{gen} \cup (x - \mathit{kill})
\end{aligned}$$

and so on: any $f^n(x)$ is $\mathit{gen} \cup (x - \mathit{kill})$. That is, going around a loop doesn't affect the transfer function, if it is of the *gen-kill* form. Thus,

$$\begin{aligned}
f^*(x) &= I \wedge f^1(x) \wedge f^2(x) \wedge \cdots \\
&= x \cup (\mathit{gen} \cup (x - \mathit{kill})) \\
&= \mathit{gen} \cup x
\end{aligned}$$

That is, the *gen* and *kill* sets for $f^*$ are *gen* and $\emptyset$, respectively. Intuitively, since we might not go around a loop at all, anything in $x$ will reach the entry to the loop. In all subsequent iterations, the reaching definitions include those in the *gen* set.

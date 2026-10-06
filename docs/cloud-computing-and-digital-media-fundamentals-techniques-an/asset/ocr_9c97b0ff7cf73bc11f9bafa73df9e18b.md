# 222 ■ Cloud Computing and Digital Media

solution. Therefore, instead of addressing the generation of $P$ directly, we introduce a tree structure, APJ tree, to represent all possible $P$'s for examination.

First, we consider how two vertices $v_i$ and $v_j$ in $G$ are selected together. If $v_i$ and $v_j$ are the nearest neighbors to each other, no other vertices need to be involved. Otherwise, $v_i$ and $v_j$ together with all the vertices residing on at least one connecting path between $v_i$ and $v_j$ need to be selected. For clear illustration purposes we introduce the Var-BQP concept, which has generalized MRJ types (covers both Pjoin and Mjoin).

**Definition 13:** $e_l^{\{var\}} = \{var\}:\{BQP\}$ is a Var-BQP entity, where $\{var\}$ represents a set of edges labeled with elements of $\{var\}$ in $G$. If $BQP \in \{BQP\}$ does not only incident to edges labeled with elements from $\{var\}$, $BQP$ is marked as optional in $\{BQP\}$, denoted by capping BQP, with a wave symbol.

For example, consider a Var-BQP entity “a:{1,2,3}” from Figure 9.8. BQP 2 and 3 are not only incident to edges labeled with “a,” they are considered to be optimal and capped with the wave symbol. Now we can answer the one-step selection condition of vertices $v_i$ and $v_j$ with the Var-BQP concept. Selecting $v_i$ and $v_j$ to compose an MRJ is equivalent to selecting a Var-BQP entity $e$, where $v_{i,j} \in [BQP]$. As described in Section 3, MRJs are identified by iteratively selecting and marking vertices from $G$ until all BJs are marked. Correspondingly, it is an iterative procedure of Var-BQP entities until all BKPs are selected. Then we first define the generic semantic of Var-BQP entities and present steps to build the APJ tree based on the join of Var-BQP entities. We then prove that all possible selection of MRJs are derived from the APJ tree.

**Definition 14:** Two Var-BQP entities $e_i^{\{var\}} = \{var\}:\{BQP_i\}$, and $e_j^{\{var\}} = \{var\}:\{BQP_j\}$ can be joined together if and only if $\{var\} \in \{var\}\pi_i$ or $BQP \in \{BQP\}\pi_j$. Join of two joinable Var-BQP entities is defined as:

```
$e_i^{\{var\}} \bowtie e_j^{\{var\}} = (\{var\}:\{BQP_i\}:\{var\}:\{BQP_j\}) \quad (9.11)
```

Intuitively, if $e_i^{\{var\}}$ and $e_j^{\{var\}}$ do not share a common variable, then there is no index of join. Furthermore, if they do not share a common BQP, there is no overlapping of source data. Thus, the join of $e_i^{\{var\}}$ and $e_j^{\{var\}}$ is logically invalid.
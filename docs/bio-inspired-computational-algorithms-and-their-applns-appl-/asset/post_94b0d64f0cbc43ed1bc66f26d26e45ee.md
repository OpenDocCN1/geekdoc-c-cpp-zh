
**Network operators of alike structure** are alike network operators that differ in unary and binary operations.

**Variation of network operator** is the change of network operator that leads to a similar network operator.

**Simple variation of network operator** is a variation that cannot be presented as a complex of other variations.

Simple variations of network operator are given in Table 3.

| Number of simple variation | Simple variation |
|---|---|
| 0 | replacement of unary operation on the edge |
| 1 | replacement of binary operation in the node |
| 2 | addition of the edge with a unary operation |
| 3 | deletion of the edge if the node where this edge comes in has at least one more incoming edge |
| 4 | Increase of the node number |
| 5 | Decrease of the node number |
| 6 | addition of the node with a binary operation and incoming edge with unary operation |
| 7 | deletion of the sink node with incoming edge if this edge is single. |

Table 3. Simple variations of network operator

**Structural variation of network operator** is a variation that changes the set of edges of network operator.

Structural variations change the incident matrix of the graph. In the Table 3 structural variations are 2 - 5. Variations 0, 1 do not change the incident matrix and lead to network operators of alike structure.

**A complete network operator** is a network operator in which we cannot perform variation 2.

A complete network operator contains L nodes in which the number of source nodes is N + P , maximum number of edges is equal to

|C| = (L - N - P)(L + N + P - 1)/2.   (12)

If we apply variation 2, addition of an edge, to any network operator, then we can construct a full network operator which is alike initial network operator.

If we apply variation 3, deletion of an edge, to the complete network operator, then we can construct any alike network operator.

Any variation of network operator can be performed by a finite number of simple variations.

## An eigen variation of network operator is a variation that does not change the number of nodes in the network operator.

In the Table 3 eigen variations are 0 - 5.

Any eigen variation of the network operator can be performed by a finite number of simple eigen variations.

To present any simple variation we use a variation vector

**w** = [w₁, w₂, w₃, w₄]ᵀ, (13)

where w₁ is the number of variation from Table 3, w₂, w₃, w₄ are elements that integer values depend on the number of variation.

Values of elements of variation vector are given in Table 4. In case the values of elements are not defined they can take any values. For example when w₁ = 1 element w₂ can keep the number of the node where this edge comes in w₃ = w₃.

Variation of network operator is presented as

**Ψ̂** = **w** ∘ **Ψ**,

where **Ψ** is the NOM before variation is performed, **Ψ̂** is the NOM after variation was performed.

| Number of variation w₁ | Number of the node where the edge comes out | Number of the node where the edge comes in | Number of unary operation | Number of binary operation |
|---|---|---|---|---|
| 0 | w₂ | w₃ | w₄ | - |
| 1 | - | w₃ | - | w₄ |
| 2 | w₂ | w₃ | w₄ | - |
| 3 | w₂ | w₃ | - | - |
| 4 | w₂ | - | - | - |
| 5 | w₂ | - | - | - |
| 6 | w₂ | - | w₃ | w₄ |
| 7 | - | w₃ | - | - |

Table 4. Elements of variation vector

Consider examples of variations of network operator. We have a network operator that describes mathematical equation

y = \frac{q_1 x_1^3}{\sqrt[3]{x_1^2 + x_2^2}} .

Network operator matrix for the given equation is

$$\boldsymbol{\Psi} = \begin{bmatrix}0 & 0 & 0 & 1 & 0 & 0 & 0 \\ 0 & 0 & 0 & 14 & 2 & 0 & 0 \\ 0 & 0 & 0 & 0 & 2 & 0 & 0 \\ 0 & 0 & 0 & 1 & 0 & 0 & 1 \\ 0 & 0 & 0 & 0 & 0 & 15 & 0 \\ 0 & 0 & 0 & 0 & 0 & 5 & 0 \\ 0 & 0 & 0 & 0 & 0 & 0 & 1\end{bmatrix}.$$

Suppose we have a variation vector $\mathbf{w} = [2\ 4\ 6\ 2]^T$. Element $w_1 = 2$ shows that we perform addition of the edge. According to Table 3 a new edge should come out from the node 4, come in the node 6 and have unary operation 2.

As a result we have NOM

$$\tilde{\boldsymbol{\Psi}} = \mathbf{w} \circ \boldsymbol{\Psi} = \begin{bmatrix}0 & 0 & 0 & 1 & 0 & 0 & 0 \\ 0 & 0 & 0 & 14 & 2 & 0 & 0 \\ 0 & 0 & 0 & 0 & 2 & 0 & 0 \\ 0 & 0 & 0 & 1 & 0 & 2 & 1 \\ 0 & 0 & 0 & 0 & 0 & 15 & 0 \\ 0 & 0 & 0 & 0 & 0 & 5 & 0 \\ 0 & 0 & 0 & 0 & 0 & 0 & 1\end{bmatrix}.$$

NOM $\tilde{\boldsymbol{\Psi}}$ corresponds to the following mathematical equation

$$y = \frac{q_1 x_1^3}{\sqrt[3]{x_1^2 + x_2^2 + (q_1 x_3)^2}}.$$

Suppose variation vectors $\mathbf{w}^1 = [0\ 4\ 7\ 11]^T$ and $\mathbf{w}^2 = [0\ 6\ 7\ 1]^T$ are given. The first component of these vectors $w_1 = 0$ shows the replacement of unary operation on the edge. The second and third components show the edge between the nodes. The first vector points to the edge $(4,7)$, the second - to the edge $(6,7)$. The fourth element contains the number of new unary operation. According to Table 1 this operation for vector $\mathbf{w}^1$ is $\rho_{11}(z)=\cos(z)$, for vector $\mathbf{w}^2$ is $\rho_1(z)=z$. As a result we obtain NOM

$$\tilde{\boldsymbol{\Psi}} = \mathbf{w}^2 \circ \mathbf{w}^1 \circ \boldsymbol{\Psi} = \begin{bmatrix}0 & 0 & 0 & 1 & 0 & 0 & 0 \\ 0 & 0 & 0 & 14 & 2 & 0 & 0 \\ 0 & 0 & 0 & 0 & 2 & 0 & 0 \\ 0 & 0 & 0 & 1 & 0 & 0 & 11 \\ 0 & 0 & 0 & 0 & 0 & 15 & 0 \\ 0 & 0 & 0 & 0 & 0 & 0 & 1 \\ 0 & 0 & 0 & 0 & 0 & 0 & 1\end{bmatrix}.$$

NOM $\tilde{\boldsymbol{\Psi}}$ corresponds to

$y = \cos(q_1 x_1^3) \sqrt[3]{x_1^2 + x_2^2}$

Consider the examples of improper variations that change the number of nodes in the network operator. We have a variation vector $\mathbf{w} = [6\ 4\ 7\ 0]^T$. Number of variation $w_1 = 6$ shows that we add the node with binary operation $w_4 = 0$ and an outgoing edge with unary operation $w_3 = 7$. After variation we obtain the NOM

$\tilde{\mathbf{\Psi}} = \mathbf{w} \circ \mathbf{\Psi} = \begin{bmatrix}0&0&0&1&0&0&0&0&0\\0&0&0&14&2&0&0&0&0\\0&0&0&0&2&0&0&0&0\\0&0&0&1&0&0&1&7&0\\0&0&0&0&0&15&0&0&0\\0&0&0&0&0&5&0&0&0\\0&0&0&0&0&0&0&0&0\\0&0&0&0&0&0&0&0&0\end{bmatrix}$

This NOM corresponds to the graph with two sink nodes and it presents at least two mathematical equations

$y_1 = \frac{q_1 x_1^3}{\sqrt[3]{x_1^2 + x_2^2}},\quad y_2 = \ln|q_1 x_1^3|$

Let us give variation vectors $\mathbf{w}^1 = [3\ 6\ 7\ 0]^T$ and $\mathbf{w}^2 = [5\ 7\ 0\ 0]^T$. In the first vector $w_1^1 = 3$, that is why we delete the edge between nodes $w_2^1 = 6$ and $w_3^1 = 7$. In the second vector $w_1^2 = 5$, and we delete the node $w_2^2 = 7$ with its incoming edge. As a result we have

$\tilde{\mathbf{\Psi}} = \mathbf{w}^2 \circ \mathbf{w}^1 \circ \mathbf{\Psi} = \begin{bmatrix}0&0&0&1&0&0\\0&0&0&14&2&0\\0&0&0&0&2&0\\0&0&0&1&0&0\\0&0&0&0&0&15\\0&0&0&0&0&0\end{bmatrix}$

This NOM corresponds to two mathematical equations $y_1 = q_1 x_1^3,\quad y_2 = \sqrt[3]{x_1^2 + x_2^2}$. Since we have changed the graph we obtain two mathematical equations. Network operator is presented on Fig. 8. Performance of variations is not always possible. If variation cannot be done then it is omitted. For example we have a variation vector $\mathbf{w} = [0\ 4\ 6\ 2]^T$. The first component shows variation 0, replacement of unary operation. However there is no edge between nodes $w_2 = 4$ and $w_3 = 6$, that is why this variation is not performed and NOM is not changed $\tilde{\mathbf{\Psi}} = \mathbf{w} \circ \mathbf{\Psi}$.

For proper variations variation w₁ = 3 is not performed if one of the following conditions is fulfilled:

- edge {w₂,w₃} is absent;
- there are no other incoming edges to the node where the edge {w₂,w₃} comes in;
- there are no other outgoing edges from the node where the edge {w₂,w₃} comes out.

A structural distance between two similar network operators is a minimal number of single variations that should be performed to obtain one network operator from the other. A structural distance between network operator Ψ¹ and network operator Ψ² is equal to a structural distance between network operators Ψ² and Ψ¹.

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_45_0.png)

Fig. 8. Network operator after variations

## 8. Search of optimal mathematic equation

Let us formulate the problem of search of optimal mathematical equation g(x,q). It is necessary to find mathematical equation g(x,q), that provides minimums of object functions with restrictions

min f_i(x,g(x,q)), i=0,D, (14)
f_i(x,g(x,q)) ≤0, j=D+1,K, (15)

where x is a vector of variables, q is a vector of parameters.

The solution to the problem (14), (15) is a mathematical equation g~(x,q). Mathematical equation g(x,q) is a function

g(x,q)=[g₁(x,q)...g_M(x,q)]^T. (16)

If D ≥1, then the solution of the problem is a Pareto set

Π={g^k(x,q): k=1,s},

where ∀g^k(x,q)∈Π ∃g^j(x,q)∈Π, f_i^*(g^j(x,q))≤f_i^*(g^k(x,q)), 0≤i≤D,
f^*(g(x,q))=[f₀(g(x,q))...f_D(g(x,q))]^T, if f_i(g^k(x,q))≤f_i(g^j(x,q)), i=0,D, and ∃_j f_i(g^k(x,q))<f_i(g^j(x,q)).

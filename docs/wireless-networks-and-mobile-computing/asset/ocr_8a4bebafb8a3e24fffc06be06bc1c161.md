node in the network effectively implies a broadcast of these two sets, if every node were to locally compute the stable regions of residence, the problem maps to that of an all-to-all broadcast of the set $RR_i$ and status (whether its a reference node) of each node $i$ in the system. Each node, on receiving this information from a neighbor, would attach its own $RR_i$ set and its status and broadcast the message again. □

# 4.5.2  Region Estimation Algorithm

Every node in a network maintains a local variable $status$ which is set to 1 if the node is a reference node and zero otherwise. Initially, the minimum regions of residence of all non-reference nodes are assumed to be infinity. Each node $i$ performs ranging with its neighbors to obtain a set of measured ranges $RR_i$ and $i$ then computes the viewed region of residence for every node $j \in N(i)$. Node $i$ then exchanges three pieces of information with each neighbor $j \in N(i)$: i) value of the status variable, $status_i$; ii) viewed region of residence of $j$, $R_{ji}$ and iii) area of the current minimum region of residence of $i$, $A_i$.

Let $RR_i = \{r_{ij}: j \in N(i)\}$, $\mathcal{T}$ represent a set of viewed regions of residence $R_{ij}$. Once node $i$ has its viewed region of residence $R_{ij}$ from its every neighbor $j$, it computes its current minimum region of residence using the following algorithm:

```
Function compute_region: Boolean
var $A_{old}$, $A_i$ : Real;

begin
    for each $R_{ij} \in \mathcal{T}$ such that $A_j \ne \infty$ do
        /* Compute the minimum region of residence of node $i$ from the viewed regions */
        $\mathcal{R}_i \leftarrow \mathcal{R}_i \cap R_{ij}$;
    endfor;
    $A_i \leftarrow$ Area of $\mathcal{R}_i$;
    if $A_i < A_{old}$ then return true;  /* $\mathcal{R}_i$ improved */
```
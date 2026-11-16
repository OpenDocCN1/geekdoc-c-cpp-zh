![](bbox=[0.16, 0.08, 0.83, 0.28])

Figure 13.11 If the set of conditional independencies is {I_P(X, {Y, W}), I_P(Y, {X, Z})} and we try to find a DAG faithful to P, we obtain the graph in (b), which is not a DAG.

We want to find a DAG faithful to P. Owing to Theorem 13.5, the links (edges without regard for direction) must be as shown in Figure 13.10 (a). We must have the directed edges shown in Figure 13.10 (b) because we have I_p(X, Y). Therefore, we must also have the directed edge shown in Figure 13.10 (c) because we do not have I_P(W, X). We conclude that P is faithful to the DAG in Figure 13.10 (c).

Example 13.22 Suppose V = {X, Y, Z, W} and the set of conditional independencies in P is

```
{I_P(X, {Y, W}), I_P(Y, {X, Z})}.
```

We want to find a DAG faithful to P. Owing to Theorem 13.5, we must have the links shown in Figure 13.11 (a). Now, if we have the chain X -> Z -> W, X <- Z <- W, or X <- Z -> W, then we do not have I_P(X, W). So, we must have the chain X -> Z <- W. Similarly, we must have the chain Y -> W <- Z. So, our graph must be the one in Figure 13.11 (b). However, this not a DAG. The problem here is that there is no DAG faithful to P.

Example 13.23 Suppose we have the same vertices and conditional independencies as in Example 13.22. As shown in that example, there is no DAG faithful to P. However, this does not mean we cannot find a more succinct way to represent P than using a complete DAG. P satisfies the Markov condition with each of the DAGs in Figure 13.12. That is, the DAG in Figure 13.12 (a) entails

```
{I_P(X, Y), I_P(Y, Z)}
```

and these conditional independencies are both in P, whereas the DAG in Figure 13.12 (b) entails

```
{I_P(X, Y), I_P(X, W)}
```
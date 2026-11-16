
![](img/67fa924962ee21b3590be9f3b10d9fe7_399_0.png)

Figure 13.8 If the set of conditional independencies is {I_P(X, Y)}, we must have the DAG in (b), whereas if it is ∅, we must have one of the DAGs in (a).

![](img/67fa924962ee21b3590be9f3b10d9fe7_399_1.png)

Figure 13.9 If the set of conditional independencies is {I_P(X, Y)}, we must have the DAG in (b); if it is {I_P(X, Y|Z)}, we must have one of the DAGs in (a).

**Example 13.18** Suppose V = {X, Y} and the set of conditional independencies in P is the empty set ∅. That is, there are no independencies. We want to find a DAG faithful to P. We cannot have the DAG in Figure 13.8 (b). The reason is that this DAG entails that X and Y are independent, which means that the Markov condition is not satisfied. So, we must have one of the DAGs in Figure 13.8 (a). We conclude that P is faithful to both the DAGs in Figure 13.8 (a). Note that these DAGs are Markov equivalent.

**Example 13.19** Suppose V = {X, Y, Z}, and the set of conditional independencies in P is {I_P(X, Y)}. We want to find a DAG faithful to P. There can be no edge between X and Y in the DAG owing to the reason given in Example 13.17. Furthermore, there must

![](img/67fa924962ee21b3590be9f3b10d9fe7_400_0.png)

**Figure 13.10** If the set of conditional independencies is \(I_P(X, \{Y, W\})\), \(I_P(Y, \{X, Z\})\), we must have the DAG in (c).

be edges between \(X\) and \(Z\) and between \(Y\) and \(Z\) owing to the reason given in Example 13.18. We cannot have any of the DAGs in Figure 13.9 (a). The reason is that these DAGs entail \(I_P(X,Y|Z)\), and this conditional independence is not present. So, the Markov condition is not satisfied. Furthermore, the DAGs do not entail \(I_P(X,Y)\). So, the DAG must be the one in Figure 13.9 (b). We conclude that \(P\) is faithful to the DAG in Figure 13.9 (b).

**Example 13.20** Suppose \(\mathbf{V} = \{X, Y, Z\}\) and the set of conditional independencies in \(P\) is \(\{I_P(X, Y|Z)\}\).

We want to find a DAG faithful to \(P\). Owing to reasons similar to those given before, the only edges in the DAG must be between \(X\) and \(Z\) and between \(Y\) and \(Z\). We cannot have the DAG in Figure 13.9 (b). The reason is that this DAG entails \(I(X, Y)\), and this conditional independence is not present. So, the Markov condition is not satisfied. So, we must have one of the DAGs in Figure 13.9 (a). We conclude that \(P\) is faithful to all the DAGs in Figure 13.9 (a).

We now state a theorem whose proof can be found in [Neapolitan, 2004]. At this point your intuition should suspect that it is true.

**Theorem 13.15** If \((G, P)\) satisfies the faithfulness condition, then there is an edge between \(X\) and \(Y\) if and only if \(X\) and \(Y\) are not conditionally independent given any set of variables.

**Example 13.21** Suppose \(\mathbf{V} = \{X, Y, Z, W\}\) and the set of conditional independencies in \(P\) is \(\{I_P(X, Y),\ I_P(W, \{X, Y\}|Z)\}\).

![](img/67fa924962ee21b3590be9f3b10d9fe7_401_0.png)

Figure 13.11 If the set of conditional independencies is {I_P(X, {Y, W}), I_P(Y, {X, Z})} and we try to find a DAG faithful to P, we obtain the graph in (b), which is not a DAG.

We want to find a DAG faithful to P. Owing to Theorem 13.5, the links (edges without regard for direction) must be as shown in Figure 13.10 (a). We must have the directed edges shown in Figure 13.10 (b) because we have I_P(X, Y). Therefore, we must also have the directed edge shown in Figure 13.10 (c) because we do not have I_P(W, X). We conclude that P is faithful to the DAG in Figure 13.10 (c).

Example 13.22 Suppose V = {X, Y, Z, W} and the set of conditional independencies in P is

```
{I_P(X, {Y, W}), I_P(Y, {X, Z})}.
```

We want to find a DAG faithful to P. Owing to Theorem 13.5, we must have the links shown in Figure 13.11 (a). Now, if we have the chain X -> Z -> W, X <- Z <- W, or X <- Z -> W, then we do not have I_P(X, W). So, we must have the chain X -> Z <- W. Similarly, we must have the chain Y -> W <- Z. So, our graph must be the one in Figure 13.11 (b). However, this is not a DAG. The problem here is that there is no DAG faithful to P.

Example 13.23 Suppose we have the same vertices and conditional independencies as in Example 13.22. As shown in that example, there is no DAG faithful to P. However, this does not mean we cannot find a more succinct way to represent P than using a complete DAG. P satisfies the Markov condition with each of the DAGs in Figure 13.12. That is, the DAG in Figure 13.12 (a) entails

```
{I_P(X, Y), I_P(Y, Z)}
```

and these conditional independencies are both in P, whereas the DAG in Figure 13.12 (b) entails

```
{I_P(X, Y), I_P(X, W)}
```

![](img/67fa924962ee21b3590be9f3b10d9fe7_402_0.png)

Figure 13.12 If the set of conditional independencies is {I_P(X, {Y, W}), I_P(Y, {X, Z})}, P satisfies the Markov condition with both these DAGs.

and these conditional independencies are both in P. However, P does not satisfy the faithfulness condition with either of these DAGs because the DAG in Figure 13.12 (a) does not entail I_P(X, W), whereas the DAG in Figure 13.12 (b) does not entail I_P(Y, Z).

Each of these DAGs is as succinct as we can represent the probability distribution. So, when there is no DAG faithful to a probability distribution P, we can still represent P much more succinctly than we would by using the complete DAG. A structure learning algorithm tries to find the most succinct representation. Depending on the number of alternatives of each variable, one of the DAGs in Figure 13.12 may actually be a more succinct representation than the other because it contains fewer parameters. A constraint-based learning algorithm could not distinguish between the two, but a score-based one could. See [Neapolitan, 2004] for a complete discussion of this matter.

## 13.3.2 Learning a DAG in which P Is Embedded Faithfully

In a sense, we compromised in Example 13.23 because the DAG we learned did not entail all the conditional independencies in P. This is fine if our goal is to learn a Bayesian network that will later be used to do inference. However, another application of structure learning is causal learning, which is discussed in the next section. When we are learning causes we would be better to find a DAG in which P is embedded faithfully. We discuss embedded faithfulness next.

**Definition 13.2** Suppose we have a joint probability distribution P of the random variables in some set V and a DAG G = (W, E) such that V ⊆ W. We say that (G, P) satisfy the embedded faithfulness condition if all and only the conditional independencies in P are entailed by G, restricted to variables

![](img/67fa924962ee21b3590be9f3b10d9fe7_403_0.png)

Figure 13.13 If the set of conditional independencies in P is {I_P(X, {Y, W}), I_P(Y, {X, Z})}, then P is embedded faithfully in this DAG.

in V. Furthermore, we say that P is embedded faithfully in G.♦

**Example 13.24** Again suppose V = {X, Y, Z, W} and the set of conditional independencies in P is

{I_P(X, {Y, W}), I_P(Y, {X, Z})}.

Then P is embedded faithfully in the DAG in Figure 13.13. It is left as an exercise to show this. By including the hidden variable H in the DAG, we are able to entail all and only the conditional independencies in P restricted to variables in V. ■

## 13.4 Application: MENTOR

To illustrate Bayesian network learning, we present the details of one large-scale application.

Mani et al. [1997] developed MENTOR, a system that predicts the risk of mental retardation (MR) in infants. Specifically, the system can determine the probabilities of the child later obtaining scores in four different ranges on the Raven Progressive Matrices Test, which is a test of cognitive function. The probabilities are conditional on values of variables such as the mother's age at time of birth, whether the mother had recently had an X-ray, whether labor was induced, etc.

### 13.4.1 Developing the Network

The structure of the Bayesian network used in MENTOR was created in the following three steps:

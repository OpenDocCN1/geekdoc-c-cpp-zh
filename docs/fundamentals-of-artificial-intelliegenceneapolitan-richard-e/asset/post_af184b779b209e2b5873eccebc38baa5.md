
![](img/67fa924962ee21b3590be9f3b10d9fe7_153_0.png)

Figure 6.2 A two-node Bayesian network.

We summarize the information used in this computation in Figure 6.2, which is a two-node/variable Bayesian network. Notice that it represents the random variables HIV and ELISA by nodes in a directed acyclic graph (DAG) and the causal relationship between these variables with an edge from HIV to ELISA. That is, the presence of HIV has a causal effect on whether the test result is positive; so there is an edge from HIV to ELISA. Besides showing a DAG representing the causal relationships, Figure 6.2 shows the prior probability distribution of HIV and the conditional probability distribution of ELISA given each value of its parent HIV. In general, Bayesian networks consist of a DAG, whose edges represent relationships among random variables that are often (but not always) causal; the prior probability distribution of every variable that is a root in the DAG; and the conditional probability distribution of every non-root variable given each set of values of its parents. We use the terms node and variable interchangeably in discussing Bayesian networks.

Let's illustrate a more complex Bayesian network by considering the problem of detecting credit card fraud (taken from [Heckerman, 1996]). Suppose that we have identified the following variables as being relevant to the problem:

| Variable | What the Variable Represents |
| :--- | :--- |
| Fraud (F) | Whether the current purchase is fraudulent |
| Gas (G) | Whether gas has been purchased in the past 24 hours |
| Jewelry (J) | Whether jewelry has been purchased in the past 24 hours |
| Age (A) | Age of the card holder |
| Sex (S) | Sex of the card holder |

These variables are all causally related. That is, a credit card thief is likely to buy gas and jewelry, and middle-aged women are most likely to buy jewelry, whereas young men are least likely to buy jewelry. Figure 6.3 shows a DAG representing these causal relationships. Notice that it also shows the conditional probability distribution of every non-root variable given each set of values of its parents. The Jewelry variable has three parents, and there is a conditional probability distribution for every combination of values of those parents. The DAG and the conditional distributions together constitute a Bayesian network.

You could have a few questions concerning this Bayesian network. First, you might ask, “What value does it have?” That is, what useful information can we obtain from it? Recall how we used Bayes’ theorem to compute P(HIV =

P(F = yes) = .00001
P(F = no) = .99999

P(G = yes | F = yes) = .2
P(G = no | F = yes) = .8
P(G = yes | F = no) = .01
P(G = no | F = no) = .99

P(A = < 30) = .25
P(A = 30 to 50) = .40
P(A > 50) = .35

P(S = male) = .5
P(S = female) = .5

P(J = yes | F = yes, A = a, S = s) = .05
P(J = no | F = yes, A = a, S = s) = .95
P(J = yes | F = no, A = < 30, S = male) = .0001
P(J = no | F = no, A = < 30, S = male) = .9999
P(J = yes | F = no, A = < 30, S = female) = .0005
P(J = no | F = no, A = < 30, S = female) = .9995
P(J = yes | F = no, A = 30 to 50, S = male) = .0004
P(J = no | F = no, A = 30 to 50, S = male) = .9996
P(J = yes | F = no, A = 30 to 50, S = female) = .002
P(J = no | F = no, A = 30 to 50, S = female) = .998
P(J = yes | F = no, A = > 50, S = male) = .0002
P(J = no | F = no, A = > 50, S = male) = .9998
P(J = yes | F = no, A = > 50, S = female) = .001
P(J = no | F = no, A = > 50, S = female) = .999

Figure 6.3 Bayesian network for detecting credit card fraud.

positive|ELISA = positive) from the information in the Bayesian network in Figure 6.2. Similarly, we can compute the probability of credit card fraud given values of the other variables in this Bayesian network. For example, we can compute P(F = yes|G = yes, J = yes, A = < 30, S = female). If this probability is sufficiently high, we can deny the current purchase or require additional identification. The computation is not a simple application of Bayes' theorem as was the case for the two-node Bayesian network in Figure 6.2. Rather it is done using sophisticated inference algorithms.

Second, you might ask how we obtained the probabilities in the network. They can either be obtained from the subjective judgments of an expert in the area or are learned from data. (In Chapter 12 we discuss techniques for learning them from data.)

Finally, you could ask why we are including the variables for age and sex in the network when the age and sex of the card holder has nothing to do with whether the card has been stolen (fraud). That is, fraud has no causal effect on the card holder's age or sex, and vice versa. The reason we include these variables is because fraud, age, and sex all have a common effect, namely the

![](img/67fa924962ee21b3590be9f3b10d9fe7_155_0.png)

Figure 6.4 Both graphs are directed graphs; only the one in (b) is a directed acyclic graph.

purchasing of jewelry. So, when we know jewelry has been purchased, the three variables are rendered probabilistically dependent owing to _discounting_. This is just like the situation involving the burglar, the alarm, and the earthquake. For example, if jewelry has been purchased in the past 24 hours, it increases the likelihood of fraud. However, if the card holder is a middle-aged woman, the likelihood of fraud is lessened (discounted) because such women are prone to buying jewelry. That is, the fact that the card holder is a middle-aged woman explains the jewelry purchase. On the other hand, if the card holder is a young man, the likelihood of fraud is increased because such men are unlikely to purchase jewelry.

We have informally introduced Bayesian networks, their properties, and their usefulness. Next we formally develop their mathematical properties.

## 6.2 Properties of Bayesian Networks

After defining Bayesian networks, we show how they are ordinarily represented.

### 6.2.1 Definition of a Bayesian Network

First, let’s review some graph theory. A **directed graph** is a pair (V, E), where V is a finite, nonempty set whose elements are called **nodes** (or vertices), and E is a set of ordered pairs of distinct elements of V. Elements of E are called **directed edges**, and if (X, Y) ∈ E, we say there is an edge from X to Y. The graph in Figure 6.4 (a) is a directed graph. The set of nodes in that figure is

```
V = {X, Y, Z, W},
```

and the set of edges is

```
E = {(X, Y), (X, Z), (Y, W), (W, Z), (Z, Y)}.
```

A **path** in a directed graph is a sequence of nodes \([X_1, X_2, \dots, X_k]\) such that \((X_{i-1}, X_i) \in \mathbf{E}\) for \(2 \le i \le k\). For example, \([X, Y, W, Z]\) is a path in the directed graph in Figure 6.4 (a). A **chain** in a directed graph is a sequence of nodes \([X_1, X_2, \dots, X_k]\) such that \((X_{i-1}, X_i) \in \mathbf{E}\) or \((X_i, X_{i-1}) \in \mathbf{E}\) for \(2 \le i \le k\). For example, \([Y, W, Z, X]\) is a chain in the directed graph in Figure 6.4 (b), but it is not a path. A **cycle** in a directed graph is a path from a node to itself. In Figure 6.4 (a) \([Y, W, Z, Y]\) is a cycle from \(Y\) to \(Y\). However, in Figure 6.4 (b), \([Y, W, Z, Y]\) is not a cycle because it is not a path. A directed graph \(\mathbb{G}\) is called a **directed acyclic graph** (DAG) if it contains no cycles. The directed graph in Figure 6.4 (b) is a DAG, whereas the one in Figure 6.4 (a) is not.

Given a DAG \(\mathbb{G} = (\mathbf{V}, \mathbf{E})\) and nodes \(X\) and \(Y\) in \(\mathbf{V}\), \(Y\) is called a **parent** of \(X\) if there is an edge from \(Y\) to \(X\), \(Y\) is called a **descendent** of \(X\) and \(X\) is called an **ancestor** of \(Y\) if there is a path from \(Y\) to \(X\), and \(Y\) is called a **nondescendent** of \(X\) if \(Y\) is not a descendent of \(X\) and \(Y\) is not equal to \(X\).

We can now state the following definition.

**Definition 6.1** Suppose we have a joint probability distribution \(P\) of the random variables in some set \(\mathbf{V}\) and a DAG \(\mathbb{G} = (\mathbf{V}, \mathbf{E})\). We say that \((\mathbb{G}, P)\) satisfies the **Markov condition** if for each variable \(X \in \mathbf{V}\), \(X\) is conditionally independent of the set of all its nondescendents given the set of all its parents. Using the notation established in Chapter 5, Section 5.2.2, this means that if we denote the sets of parents and nondescendents of \(X\) by \(PA_X\) and \(ND_X\), respectively, then

\(I_P(X, ND_X | PA_X)\).

If \((\mathbb{G}, P)\) satisfies the Markov condition, \((\mathbb{G}, P)\) is called a **Bayesian network**.\(\unknown\)

**Example 6.1** Recall Chapter 5, Figure 5.1, which appears again as Figure 6.5. In Chapter 5, Example 5.23, we let \(P\) assign 1/13 to each object in the figure, and we defined these random variables on the set containing the objects.

| Variable | Value | Outcomes Mapped to This Value |
|---|---|---|
| \(L\) | \(l_1\) | All objects containing an A |
| | \(l_2\) | All objects containing a B |
| \(S\) | \(s_1\) | All square objects |
| | \(s_2\) | All circular objects |
| \(C\) | \(c_1\) | All black objects |
| | \(c_2\) | All white objects |

We then showed that \(L\) and \(S\) are conditionally independent given \(C\). That is, using the notation established in Chapter 5, Section 5.2.2, we showed

\(I_P(L, S | C)\).

Consider the DAG \(\mathbb{G}\) in Figure 6.6. For that DAG we have the following.

| Node | Parents | Nondescendents |
|---|---|---|
| \(L\) | \(C\) | \(S\) |
| \(S\) | \(C\) | \(L\) |
| \(C\) | \(\emptyset\) | \(\emptyset\) |

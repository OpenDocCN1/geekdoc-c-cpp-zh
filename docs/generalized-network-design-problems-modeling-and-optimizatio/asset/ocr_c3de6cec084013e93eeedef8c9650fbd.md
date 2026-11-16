+   • $\mathcal{N}_l^k$ is the feasible neighborhood of person $k$, when at cluster $V_l$;

+   • random. is a function that randomly chooses one element from the set given as its argument.

Again, if all clusters in the candidate list have already been visited, the feasible neighborhood $\mathcal{N}_l^k$ is empty. In this case, a client that ignores the recommendation of his consultant may choose one of the clusters not in the candidate list, by using a random proportional rule similar to the one given by formula (3.24).

The personal preference of a client for a given consultant is computed as the inverse of the cost of the generalized tour that corresponds to the global tour advertised by the consultant. In conjunction with the reputation, personal preference is used by clients in order to compute the probability for choosing a given consultant $k$:

```
$$p_k = \frac{(\text{reputation}_k \times \text{preference}_k)^2}{\sum_{c \in \mathcal{C}} (\text{reputation}_c \times \text{preference}_c)^2} \quad (3.26)$$
```

where $\mathcal{C}$ is the set of all available consultants.

At each iteration, the consultant's $k$ reputation fades with a constant rate $r$:

```
$$\text{reputation}_k \leftarrow \text{reputation}_k(1 - r) \quad (3.27)$$
```

A consultant enters sabbatical mode when his reputation sinks below a minimum level. In our algorithm, this minimum reputation value is set to 1 and the duration of the sabbatical leave is set to 20 iterations. At the end of the sabbatical leave, a consultant's reputation is reset to a given value, specified by the parameter $initialReputation$.

In addition, the algorithm prevents the reputation of the best consultant from sinking below this initial value. We designate as best consultant the consultant whose strategy has led to the construction of the best-so-far solution.

Each time a client achieves a success, the reputation of his consultant is incremented. Should a client construct a best-so-far solution, the consultant's reputation receives a supplementary $bonus$. The reputation of a consultant cannot exceed the maximum value given by the parameter $maxReputation$.

# An variant of the algorithm, that uses confidence

Here, we propose a variant of our algorithm, based on the approach introduced in [87], which correlates the recommendation of a consultant with a certain level of confidence. Each arc in the global tour, advertised by a consultant, has an associated strength. Strengths are updated each time the consultant adjusts his strategy. If an arc in the newly advertised tour was also present in the old advertised tour, its strength will be incremented. Otherwise, its strength is set to 0. The strength of an arc could be interpreted as the consultant's confidence in recommending this arc to a client. A client is more likely to accept recommendations made with greater confidence.
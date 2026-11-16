![](bbox=[0.27, 0.08, 0.75, 0.4])

Figure 7.4 The Markov condition entails \( I_P(W, X) \) for this DAG.

| Conditional Independence | Reason Conditional Independence Is Not Entailed |
|---|---|
| \( I_P(X, Y | H) \) | \( [X, B, C, D, Y] \) is not blocked |
| \( I_P(X, Y | D) \) | \( [X, F, H, I, Y] \) is not blocked |
| \( I_P(X, Y | \{H, C, K\}) \) | \( [X, J, K, L, Y] \) is not blocked |
| \( I_P(X, Y | \{H, C, M\}) \) | \( [X, J, K, L, Y] \) is not blocked |

**Example 7.4** Owing to Theorem 7.1, the Markov condition entails the following conditional independence for the DAG in Figure 7.4.

| Conditional Independence | Reason Conditional Independence Is Entailed |
|---|---|
| \( I_P(W, X) \) | \( [W, Y, X] \) is blocked at \( Y \) \
| | \( [W, Y, R, Z, X] \) is blocked at \( R \) \
| | \( [W, Y, R, S, Z, X] \) is blocked at \( S \) |

Note that \( I_P(W, X) \) is the same as \( I_P(W, X | \varnothing) \), where \( \varnothing \) is the empty set, and \( Y \), \( R \), \( S \), and \( T \) are all not in \( \varnothing \).

# 7.2 Faithfulness

Recall that a DAG entails a conditional independence if every probability distribution, which satisfies the Markov condition with the DAG, must have the conditional independence. Theorem 7.1 states that all and only d-separations
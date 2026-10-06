# Markov Chains

![](bbox=[0.14, 0.07, 0.86, 0.301])

**Figure 6.3** Communication diagram and eigenvalues for a four-state Markov chain.

# ### 6.3.1 Example

Matlab's memoir command is a convenient way to randomly generate transition matrices with a given structure. Here is one example with $m=4$ states, in the five zeros in the transition matrix were imposed:

```
$P = \begin{pmatrix} 0.0500 & 0 & 0.5536 & 0.3964 \ 0.0094 & 0.0500 & 0 & 0.0406 \ 0.1519 & 0 & 0.8481 & 0 \ 0 & 0.1891 & 0.4302 & 0.3807 \end{pmatrix} (6.21)$
```

The plot on the left in Figure 6.3 shows the communication diagram for this Markov chain. This is a directed graph in which nodes correspond to the four states, and there is a directed edge between $x$ and $y$ if $P(x,y) > 0$. It is a generalization of the graph model for deterministic control systems introduced in Example 3.2.

The eigenvalues of $P$ are $\{\lambda_1, \dots, \lambda_4\} = \{1.5004, -0.0878 \pm 0.3295j\}$. The spectral gap is defined by $1 - \max\{|lambda_i| : i \geq 2\} = 1 - |\lambda_2|$. The plots were obtained using Matlab commands graphplot and eigplot. Matlab can be used to find the eigenvalues of the transpose of $P$:

```
[V, L] = \text{eig}(P^T)$
```

which gives $L=\{\lambda_1, \dots, \lambda_4\}$ and the columns of $V$ are the corresponding eigenvectors of $P^T$. From this we obtain the invariant measure, $\pi = [0.1378, 0.0178, 0.0755, 0.0893]$.

Theorem 6.2 states $P^n(x,y) \to \pi(y)$ at rate approximately $|\lambda_2| = \rho^n$ for all $x,y$. Shown in Figure 6.4 is a plot of $\log(|P^n(x,y) - P^n(y,y)|)$ for $y=4$ and $x \neq 4$, along with a plot of $\log(|\lambda_2|) = n \log(\rho)$. Observe that the difference $|P^n(x,y) - P^n(y,y)| - n \log(\rho)$ is bounded in $n$ (which is more than anticipated from (6.18)). This bound holds in example because there is a single eigenvalue satisfying $|\lambda_2| = \rho$.
# 9.8 GQ and Zap

This section contains more ideas to accelerate Watson's Q-learning, and also inspire new techniques for using outside of the tabular setting. However, theory in this section is restricted to the tabular basis.

An understanding of the matrix chain algorithms requires a closer look at the vector field $f^0$ given in Proposition 9.15.

When the state and input space are finite as assumed here, these $\{\Phi^m : 1 \le m \le M\}$, where $M$ is the number of possible functions from X to U. For each $m$, denote

```
$$\Theta^m = {\theta \in \mathbb{R}^d : \Phi^m(x) \in \arg \min H^	heta(x,u) \text{ for each } x\}$
```

Each $\Theta^m$ is a convex cone: $r_1\theta^1 + r_2\theta^2 \in \Theta^m$ whenever $	heta^1 \in \Theta^m$ and $r_i \in \mathbb{R}_+$ for $i=1,2$. Figure 9.4 provides an illustration of these sets.

Let $Q^m$ denote the fixed-Q-function with policy $\Phi^m$. Denoting by $T_m$ the transition matrix for the representing Markov chain $\Phi$ with control $\Phi^m$, we have

```
$Q^m = [I - \gamma T_m]^{-1}c$.
```

![](bbox=[0.134, 0.383, 0.403, 0.58])

These Q-functions are also indicated in Figure 9.4, which is justified by the identity (9.73). The index $m^*$ is special because $Q^{m^*} \in \Theta^{m^*}$ which implies the fixed-point equation:

```
$$\Phi^{m^*}(x) \in \arg \min Q^{m^*}(x,u) \text{ for each } x \in X$.
```

That is, this of policy iteration returns the same policy, which implies that $Q^{m^*} = Q^*$. Let II denote the diagonal matrix $\Pi = \text{diag}(\alpha)$ (also equal to $R^
abla$) in (9.78).

**Lemma 9.25** The Jacobian $A = \partial f^0$ is piecewise, with $A(\theta)$ independent of $\theta$ within the interior of $\Theta^m$ for each $m$. If $\theta \in \mathbb{R}^d$ satisfies $\theta \in \text{interior}(\Theta^m)$ for any $m$, then at this value the Jacobian is given

```
$A(\theta) = -\Pi[I - \gamma T_m] \quad (9.92a)
```

```
With $T_m(i,j) \overset{mat}{==} P_w(x^i,x^j)\}\{u^j = \Phi^m(x^j)\}, \quad 1 \le i,j \le d$.
```

The function $f^0$ is thus continuous and piecewise linear, and for each,

```
$f^0(\theta) = A(\theta) - \Pi b, \quad b_i = -c(x^i,u^i) \text{ for each } i. \quad (9.92b)
```
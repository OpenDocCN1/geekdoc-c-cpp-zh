# C.2 A Fully Observed MDP

setting, we require a sufficient statistic $I=\{I_0, \dots, I_n, \dots\}$ evolving over some fixed space, such that for some function $V_{n,N}^*$,

$V_{n,N}^* = V_{n,N}(I_n).

Since this is a time-homogeneous model, we might hope to have $V_{n,N}^* = V_{N-n}(I_n)$ for a sequence of functions $\{V_m^* : m \ge 0\}$.

The amazing conclusion is: A sufficient statistic exists, with $I_n=b_n$, for which the belief $b_n$ is sometimes called the information state. Moreover, the stochastic process $b=\{b_0,b_1,...\}$ is itself a controlled Markov model that is fully observed. The Markov property is explained in Proposition C.1. A deterministic stationary Markov policy is defined via a feedback loop $U=\Phi(b)$, where $\Phi: S \to U$.

Proposition C.1 states that for each such that $n \ge 0$,

```
$b_{n+1} = \mathcal{M}(b_n, Y_{n+1}), \quad n \ge 0. \quad (C.8)
```

From this, a specific formula for the controlled transition kernel for $\{b_n\}$ is obtained in (C.9). The proof is postponed to Section C.3

**Proposition C.1 (Transition Law for the Belief State)** The following Markov properties hold: for any admissible input $U$, any set $S \subset S$, and any $y' \in Y$.

```
$P(b_{n+1} \in S, Y_{n+1} = y' | Y_n) = P(b_{n+1} \in S, Y_{n+1} = y' | b_n, U_n),$
```

```
$P(b_{n+1} \in S | U_n) = P(b_{n+1} \in S | b_n, U_n).
```

The transition kernel for the belief state is given as follows: for any $b \in S, u \in U$, and any $S \subset S$,

```
$P(b_{n+1} \in S, b_n=b, U_n=u) = \sum_{y'} \mathbb{1}\{\mathcal{M}(b,y',u) \in S\} P(Y_{n+1}=y' | b_n=b, U_n=u)$,
$$\sum_{y'} \mathbb{1}\{\mathcal{M}(b,y',u) \in S\} \left( \sum_{x,x' \in X} b(x)P_u(x,x')q(y' | x') \right). \quad (C.9)$
```

Moreover, for any function $F: S \times Y \to \mathbb{R

```
$E[F(b_{n+1}, Y_{n+1}) | Y_n; b_n=b, U_n=u] = \sum_{y'} \sum_{x'} b(x)P_u(x,x')q(y' | x')F(\mathcal{M}(b,y',u)).
```

The representation of the cost to go is given in the following:

**Proposition C.2** For any $b \in S$ and $u \in U$, denote the following:

```
$C(b,u) \stackrel{\text{def}}{=} \sum_x b(x)c(x,u), \quad \mathcal{V}_0(u) \stackrel{\text{def}}{=} \sum_x b(x)V_0(x). \quad (C.10)
```
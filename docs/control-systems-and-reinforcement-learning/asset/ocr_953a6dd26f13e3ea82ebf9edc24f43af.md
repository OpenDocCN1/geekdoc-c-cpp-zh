Linear and Time Invariant Model. The most successful class of absurdly simple models are linear and time invariant (LII). The general scalar LII model is defined by a sequence of scalars $\{b_i\}$ (impulse response), and for a scalar input sequence $u$, the model defines $y(k)$ as the sum

```
y(k) = \sum_{i=0}^{k} b_i u(k-i), \quad k \geq 0.
```

This is in fact too complex in many situations. A more tractable subclass of LII models are auto-regressive moving-average (ARMA): for scalar coefficients $\{a_i, b_i\}$,

```
y(k) = -\sum_{i=1}^{N} a_i y(k-i) + \sum_{i=0}^{M} b_i u(k-i), \quad k \geq 0.
```

A linear input-output model motivates the design of a policy $\phi$ that has a similar linear form. A common design technique based on optimization will be described in the following chapters, beginning in Section 3.6.

# 2.3 State Space Models

# 2.3.1 Sufficient Statistics and the Nonlinear State Space Model

In statistics, the term sufficient statistic is used to denote a quantity that summarizes all past observations. The state plays an analogous role in control theory.

A state space model requires the following ingredients: the state space $X$ on which the state $x$ evolves, and an input space (or action space) on which the input $u$ evolves. We may have additional constraints coupling the state and the input, which is modeled via

```
u(k) \in U(x), \quad when x(k) = x \in X,
```

with $u(x) \subseteq U$ for each $x$. We might want to model an observation process $y$ evolving on a set $Y$. In the control theory literature, it is common to assume that $X, U$, and $Y$ are subsets of Euclidean space, while in operations research and reinforcement learning it is more common to assume these are finite sets. However, in this book we prefer the control perspective that we can more easily search for structure of control solutions: for example, an optimal input a continuous function of the state?

We require two functions $F: X \times U \to X$ and $G: X \times U \to Y$ that define the state equations:

```
x(k+1) = F(x(k), u(k)), \quad x(0) = x_0,
```

```
y(k) = G(x(k), u(k)).
```

An LII model can be transformed into a state space model in which the two functions $F, G$ are linear in $(x, u)$.

We might allow $F, G$ to depend upon the time variable $k$. It is argued in Section 3.3 that it is often more convenient to assume that the state $x(k)$ includes $k$ as one component.
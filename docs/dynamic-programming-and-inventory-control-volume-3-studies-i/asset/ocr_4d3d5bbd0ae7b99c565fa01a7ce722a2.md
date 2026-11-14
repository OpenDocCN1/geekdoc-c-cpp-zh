# ERGODIC CONTROL IN DISCRETE TIME

We have in the preceding chapters considered always a control problem with discount \(\alpha < 1\). The problem of Ergodic Control corresponds to the case when \(\alpha = 1\). This is a limit situation, we cannot just take \(\alpha = 1\) in the formulas. The value function becomes infinite. We have studied in Chapter 3 the situation without control. We develop in this Chapter the corresponding theory for controlled Markov chains.

# 6.1. FINITE NUMBER OF STATES

We study here the simplest case of a Markov chain with a finite number of states.

# 6.1.1. ASSUMPTIONS-NOTATION.

We consider a Controlled Markov chain with a finite number of states. The space of states is denoted by \(X\) and the transition probability reduces to a matrix, which is defined by \(\varpi^u(i, j) = P(y_{n+1} = j | y_n = i)\), where \(y_n\) represents the canonical process (the state of the system at time \(n\)). The control \(v \in U\). We assume

+   (6.1.1)
+   U compact
+   \(\varpi^u(i, j)\) is continuous in \(v, \forall i, j\)
+   \(\varpi^u(i, j) > 0, \forall i, j, v\)

Note that this assumption implies a uniform bound below, since we have a finite number of functions which are strictly continuous on a compact. We write

```
(6.1.2) \(\varpi^u(i, j) \ge \delta > 0.\)
```

We denote by \(\Phi^u\) the operator associated with the matrix \(\varpi^u\). We recall that

```
\(\Phi^u f(i) = \sum_j \varpi^u(i, j) f(j).\)
```

This formula extends to a feedback \(v(.)\). We will define \(\Phi^{v(.)} f\) by

```
\(\Phi^{v(.)} f(i) = \sum_j \varpi^{v(i)}(i, j) f(j).\)
```

To the operator \(\Phi^{v(.)}\) is associated the transition matrix \(\varpi^{v(i)}(i, j)\). We clearly have the property

```
(6.1.3) \(\varpi^{v(i)}(i, j) \ge \delta, \forall i, j\)
```

Again we can study directly the problem of existence and uniqueness of the invariant measure. We look for a density \( m(x) \) with respect to Lebesgue measure on \( X \). This density must satisfy the equation

\[ m(\eta) = \int_{-\infty}^S m(x)\varpi(x, \eta) dx, \]

which amounts to

\[ m(\eta) = f(S-\eta) \int_{-\infty}^{-s} m(x) dx + \int_s^S m(x) f(x-\eta) \mathbb{1}_{\{\eta \le x\}} dx \]

### Exercise 3.5. Show that \( m(\eta) \) is uniquely defined by the formulas

\[ m(\eta) = \frac{f(S-\eta) + \int_s^S u(x) f(x-\eta) dx}{1 + \int_s^S u(y) dy}, \text{ if } \eta \le s \]

\[ m(\eta) = \frac{u(\eta)}{1 + \int_s^S u(y) dy}, \text{ if } s \le \eta \le S \]

where the function \( u(\eta) \) is defined in \( s,S \) as the unique solution of the integral equation

\[ u(\eta) = f(S-\eta) + \int_\eta^S u(x) f(x-\eta) dx, s \le \eta \le S. \]

### 3.6.3. FINITE NUMBER OF STATES.

Suppose \( X \) is composed of a finite number of states, denoted by \( i = 1, \cdots, I \). The transition probability reduces to a matrix \( \varpi(i, j) \). In order to apply Exercise 3.3 it is sufficient to assume that there exists a state \( j_0 \) such that

(3.6.8) \( \varpi(i, j_0), \forall i \in X. \)

The unique invariant measure will satisfy

\[ m_i = \sum_j m_j \varpi(j, i), \sum_i m_i = 1, m_i \ge 0 \]

## OPTIMAL CONTROL IN DISCRETE TIME

A very comprehensive presentation of Discrete-Time Markov Control Processes can be found in the book of O. Hernández-Lerma and J.B. Lasserre, [25]. Our presentation discusses more completely the issue of uniqueness, and separates completely the study of the functional equation, resulting from Dynamic Programming (Bellman equation) from its interpretation in the context of optimal control.

### 4.1. DETERMINISTIC CASE

### 4.1.1. NOTATION.

We begin with deterministic models, although the deterministic case can be embedded in the stochastic case. The reason is because in deterministic situations one does not have to worry about information. Decisions are just given values (open loop control). In the stochastic case, decisions are functions of the state of information (closed loop control). It is possible to reconcile the two approaches in the deterministic case, but this is unnecessarily complex just to obtain the major results.

We consider a dynamic system whose evolution is governed by

(4.1.1) 
\[ y_{n+1} = g(y_n, v_n), \quad y_1 = x. \]

At this stage, we do not need any specific assumptions on the function g, except measurability. As we shall see the first part of the discussion will be of algebraic nature. The state space is X, a metric space R^d or a discrete space. We next consider a function

(4.1.2) 
\[ l(x, v) \text{ bounded below.} \]

A control (or more precisely a control policy) is a sequence of values v_1 ... v_n ... in a subset U of a metric space. A control is denoted by V. We define the payoff

(4.1.3) 
\[ J_x(V) = \sum_{n=1}^{\infty} \alpha^{n-1} l(y_n, v_n). \]

Without loss of generality, we will assume l(x, v) >= 0. Indeed, if l(x, v) + C >= 0, we can change J_x(V) into J_x(V) + C / (1 - alpha) and obtain the positivity assumption. The discount alpha is smaller than 1. We define

(4.1.4) 
\[ u(x) = \inf_V J_x(V), \]

which is a positive number. The function u(x) is called the value function. We shall assume that

(4.1.5) 
\[ u(x) < \infty \]

### 4.1.2. BELLMAN EQUATION.

The function u(x) satisfies a functional equation, called Bellman equation, [2], [11]. As we shall see, it is simply the consequence of algebraic considerations. The study of this functional equation, independently of its origin, will be done later and requires analysis tools.

### Proposition 4.1.

The function u(x) satisfies the relation

(4.1.6) 
\[ u(x) = \inf_{v \in U} [l(x, v) + \alpha u(g(x, v))]. \]

PROOF. From the definition, we can write

\[ u(x) = \inf_{v_1} \left[ l(x, v_1) + \alpha \inf_{v_2 \cdots v_n} \left[ \sum_{n=2}^\infty \alpha^{n-2} l(y_n, v_n) \right] \right], \]

but the inf inside the bracket is clearly u(g(x, v)). Therefore the result follows.

Suppose now that there exists a measurable function \(\hat{v}(x)\) such that the infimum in the right hand side of (4.1.6) is attained for this value and for any value of x. Such a function is called a feedback. We can use this feedback in the state equation and define a sequence \(\hat{y}_n\) as follows

\[ \hat{y}_{n+1} = g(\hat{y}_n, \hat{v}(\hat{y}_n)). \]

Defining next \(\hat{v}_n = \hat{v}(\hat{y}_n)\) we obtain a control \(\hat{V} = (\hat{v}_1 \cdots \hat{v}_n \cdots)\). We then obtain the result

### Proposition 4.2.

\(\hat{V}\) is optimal.

PROOF. By induction we can check that

\[ u(x) = \sum_{j=1}^n \alpha^{n-1} l(\hat{y}_n, \hat{v}_n) + \alpha^n u(\hat{y}_{n+1}), \]

and thus u(x) \(\ge J_x(\hat{V})\). However being the infimum, u(x) is also smaller than \(J_x(\hat{V})\). So we have equality and thus \(\hat{V}\) is optimal.

Note that the optimal control is obtained via a feedback on the state. This property is a curiosity in the deterministic case, but will play a fundamental role in the stochastic case, since it has an informational content.

### 4.1.3. EXTENSION WHEN THE SET OF CONSTRAINTS DEPENDS ON THE STATE.

There is however a case when information matters, even in the deterministic case. It is the case when the set of constraints U is not fixed, but depends on the state U(x). A control policy V cannot be a simple sequence v_n of elements of U, because U is not fixed anymore. We must also satisfy v_n \in U(y_n).

However, it is not difficult to check that the argument of the proof of Proposition 4.1 remains valid. The Bellman equation is changed into

(4.1.7) 
\[ u(x) = \inf_{v \in U(x)} [l(x, v) + \alpha u(g(x, v))]. \]

### 4.2. STOCHASTIC CASE: GENERAL FORMULATION

We turn now to the stochastic case. As we shall see the machinery is more complex.

### 4.2.1. NOTATION AND ASSUMPTIONS.

The probabilistic set up is the same as in Chapter 3. The state space is X, and the probability space is $\Omega = \mathcal{X}^N$, with $\sigma$-algebra $\mathcal{A} = \mathcal{X}^N$. The canonical process is denoted by $y_n(\omega) = \omega_n$, and it generates the filtration $\mathcal{Y}^n$. We now consider a family of transition probabilities, indexed by a parameter $v$, the control variable. The parameter $v$ belongs to a set $U$, the set of controls, which is a closed subset of a metric space.

The transition probability is denoted $\pi(x, v, dy)$. We associate to it the operator on B (space of measurable bounded functions on X), also indexed by v

\(\Phi^v f(x) = \int_X f(y) \pi(x, v, dy).\)

We now define as a control policy a sequence of Borel maps with values in U

$v_1(\eta_1), v_2(\eta_1, \eta_2)$

\(\cdots, v_n(\eta_1, \cdots, \eta_n), \cdots\)

Such a control is denoted by V. However, we see the main difference with the deterministic case, in which a control was simply a sequence of values. In the stochastic case, the control must be defined in a closed loop manner.

To a control V and an initial state x we associate a probability law on $\Omega$, $\mathcal{A}$ which is the conditional law of the canonical process given $y_1 = x$. We denote it by $P^{V,x}$. For any test function $f(x_1, \cdots, x_n)$ we have

$E^{V,x} f(y_1, \cdots, y_n) = E[f(y_1, \cdots, y_n) | y_1 = x]$
$= \int \pi(x, v_1(x), dx_2) \int \pi(x_2, v_2(x, x_2), dx_3) \cdots$
$\int \pi(x_{n-1}, v_{n-1}(x, x_2, \cdots, x_{n-1}), dx_n) f(x_1, \cdots, x_n).$

$P^{V,x}$ is a controlled Markov chain. A controlled Markov chain is not a Markov chain strictly speaking, since we keep memory of all previous states, because of the decision rule. However some analogy with the standard Markov chains can be made. We introduce

$P^{V,x}(n-1; x, \cdots, x_{n-1}, n; \Gamma) = \pi(x_{n-1}, v_{n-1}(x, x_2, \cdots, x_{n-1}), \Gamma)$

$P^{V,x}(m; x, \cdots, x_m; n; \Gamma) = \int \pi(x_m, v_m(x, x_2, \cdots, x_m), dx_{m+1} \cdots$
$\int \pi(x_{n-2}, v_{n-2}(x, x_2, \cdots, x_{n-2}), dx_{n-1} \pi(x_{n-1}, v_{n-1}(x, x_2, \cdots, x_{n-1}), \Gamma)$

### Exercise 4.1. Check that

$P^{V,x}(k; y_1, \cdots, y_k; k+n, \Gamma) = E^{V,x}[\mathbb{I}_{\Gamma}(y_{k+n}) | \mathcal{Y}^k],$

which can be extended to replacing $k$ by a stopping time $\nu$. Check that

$P^{V,x}(\nu; y_1, \cdots, y_\nu; \nu+n, \Gamma) = E^{V,x}[\mathbb{I}_{\Gamma}(y_{\nu+n}) | \mathcal{D}^\nu]$

Check that for any $u \in B$

$u(y_n) + \sum_{j=1}^{n-1} (u(y_j) - \Phi^{v_j}(y_1, \cdots, y_j) u(y_j)),$

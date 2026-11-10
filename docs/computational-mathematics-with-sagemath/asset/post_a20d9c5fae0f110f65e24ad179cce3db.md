
A solver object enables us to register the definition and the parameters of the system we want to solve; it gives access to the numerical tools for solving differential equations from the GSL library, already mentioned for numerical quadrature.

The system equations are given in the form of a function:

```python
sage: def f_1(t,y,params): return [y[1],params[0]*(1-y[0]^2)*y[1]-y[0]]
sage: T.function = f_1
```

The parameter y represents the vector of unknown functions, and we should return the right-hand side vector of the system, in terms of t and an optional parameter (here params[0] which represents $\mu$).

Some of the GSL algorithms require the system Jacobian as well (the matrix whose $(i, j)$ term is $\frac{\partial f_i}{\partial y_j}$, and whose last line contains $\frac{\partial f_i}{\partial t}$):

```python
sage: def j_1(t,y,params):
....:     return [[0, 1],
....:             [-2*params[0]*y[0]*y[1]-1, params[0]*(1-y[0]^2)],
....:             [0,0]]
sage: T.jacobian = j_1
```

It is now possible to ask for a numerical solution. We choose the algorithm, the interval on which we want the solution, and the number of steps, which determines $h$:

```python
sage: T.algorithm = "rk8pd"
sage: T.ode_solve(y_0=[1,0], t_span=[0,100], params=[10],
....:           num_points=1000)
sage: f = T.interpolate_solution()
```

Here, we have chosen the Runge-Kutta Dormand-Prince algorithm to compute the solution on $[0,100]$; the initial conditions and the value of the parameters (here one only) are given too: $y_0=[1,0]$ means $y_0(0) = 1, y_1(0) = 0$, i.e., $x(0) = 1, x'(0) = 0$.

To show the graph of the solution (we might try `plot(f, 0, 2)` to see the zero derivative in $t = 0$ more clearly):

```python
sage: plot(f, 0, 100)
```

![](img/99840d73c45ee58b635c4eedc727fd9a_333_0.png)

### 14.2.2 Available Functions

We have already mentioned for the solver objects from GSL the `rk8pd` method. Other methods are available:

- `rkf45`: Runge-Kutta-Fehlberg, an adaptive method of orders 5 and 4;
- `rk2`: adaptive Runge-Kutta of orders 3 and 2;
- `rk4`: the classical Runge-Kutta method of order 4;
- `rk2imp`: an implicit order 2 Runge-Kutta method with evaluation in the middle of the interval;
- `rk4imp`: an implicit order 4 Runge-Kutta method with evaluation at “Gaussian points”⁴;
- `bsimp`: the implicit Bulirsch-Stoer method;
- `gear1`: the implicit one-step Gear method;
- `gear2`: the implicit two-step Gear method.

For more details on all these methods, we refer the reader to [AP98].

One should note that the GSL limitation to machine floating-point numbers — thus of fixed precision — that we mentioned for the numerical integration also holds for solving differential equations.

Maxima also provides routines to solve differential equations numerically, with its own syntax:

```sage
sage: t, y = var('t, y')
sage: desolve_rk4(t*y*(2-y), y, ics=[0,1], end_points=[0, 1], step=0.5)
[[0, 1], [0.5, 1.12419127424558], [1.0, 1.461590162288825]]
```

The `desolve_rk4` function uses the order-4 Runge-Kutta method (the same as `rk4` for GSL) and takes as parameters:

- the right-hand side of the equation \(y'(t) = f(t,y(t))\), here \(y' = ty(2-y)\);
- the name of the unknown function, here \(y\);
- the initial conditions `ics`, here \(t = 0\) and \(y = 1\);
- the resolution interval `end_points`, here \([0,1]\);
- the resolution step, here 0.5.

We omit the similar command `desolve_system_rk4`, already mentioned in Chapter 4, and which applies to a differential system. Maxima is limited to machine precision too.

If we want arbitrary precision solutions, we might use `odefun` from the `mpmath` package:

⁴The roots of the degree-2 Legendre polynomial, which are shifted on the interval \([t, t + h]\), and whose name makes reference to the Gauss-Legendre quadrature rule.

```sage
sage: import mpmath
sage: mpmath.mp.prec = 53
sage: sol = mpmath.odefun(lambda t, y: y, 0, 1)
sage: sol(1)
mpf('2.7182818284590451')
sage: mpmath.mp.prec = 100
sage: sol(1)
mpf('2.7182818284590452353602874802307')
sage: N(exp(1), 100)
2.7182818284590452353602874714
```

The arguments of the `mpmath.odefun` function are:

- the right-hand sides of the system of equations, in the form of a function \((t,y) \mapsto f(t,y(t))\), here \(y'=y\), like for the `ode_solver` function. The dimension of the system is automatically deduced from the dimension of the function return value;
- the initial conditions \(t_0\) and \(y(t_0)\), here \(y(0)=1\).

For example for this two-dimensional system

$$\begin{cases} y_1' &= -y_2 \\ y_2' &= y_1 \end{cases}$$

whose solutions are \((\cos(t),\sin(t))\), with initial conditions \(y_1(0)=1\) and \(y_2(0)=0\):

```sage
sage: mpmath.mp.prec = 53
sage: f = mpmath.odefun(lambda t, y: [-y[1], y[0]], 0, [1, 0])
sage: f(3)
[mpf('-0.98999249660044542'), mpf('0.14112000805986721')]
sage: (cos(3.), sin(3.))
(-0.98999249660044505, 0.141120008059867)
```

The `mpmath.odefun` function relies on Taylor’s method. For degree \(p\) it uses:

$$y(t_{n+1}) = y(t_n) + h\frac{dy}{dt}(t_n) + \frac{h^2}{2!}\frac{d^2y}{dt^2}(t_n) + \ldots + \frac{h^p}{p!}\frac{d^py}{dt^p}(t_n) + O(h^{p+1}).$$

The main question is the computation of the derivatives of \(y\). For this purpose, `odefun` computes approximate values

$$[\widetilde y(t_n+h),\ldots,\widetilde y(t_n+ph)] \approx [y(t_n+h),\ldots,y(t_n+ph)]$$

using \(p\) steps of the less precise method of Euler. We then compute

$$\frac{dy}{dt}(t_n) \approx \frac{\widetilde y(t_n+h)-\widetilde y(t_n)}{h}, \qquad \frac{dy}{dt}(t_n+h) \approx \frac{\widetilde y(t_n+2h)-\widetilde y(t_n+h)}{h}$$

then

$$\frac{d^2y}{dt^2}(t_n) \approx \frac{\frac{dy}{dt}(t_n+h)-\frac{dy}{dt}(t_n)}{h},$$

## 15 Enumeration and Combinatorics

This chapter mainly covers the treatment in Sage of the following combinatorial problems: enumeration (how many elements are there in a set $S$?), listing (generate all elements of $S$, or iterate through them), and random selection (choosing an element at random from a set $S$ according to a given distribution, for example the uniform distribution). These questions arise naturally in the calculation of probabilities (what is the probability in poker of obtaining a straight or a four-of-a-kind of aces?), in statistical physics, and also in computer algebra (the number of elements in a finite field), or in the analysis of algorithms. Combinatorics covers a much wider domain (partial orders, representation theory . . . ) for which we only give a few pointers towards the possibilities offered by Sage. Graphs are treated in Chapter 16.

A characteristic of computational combinatorics is the profusion of types of objects and sets that one wants to manipulate. It would be impossible to describe them all, or a fortiori, to implement them all. After some examples (§15.1), this chapter illustrates the underlying method: supplying the basic building blocks for describing common combinatorial sets §15.2, tools for combining them to construct new examples §15.3, and generic algorithms for solving uniformly a large class of problems §15.4. On a first reading, this chapter can be skipped through quickly, pausing at the summaries of the sections §15.1.2 and §15.3.

This is a domain in which Sage has much more extensive capabilities than most computer algebra systems, and it is rapidly expanding; at the same time, it is still quite new, and has many unnecessary limitations and inconsistencies.

### 15.1 Initial Examples

### 15.1.1 Poker and Probability

We begin by solving a classic problem: enumerating certain combinations of cards in the game of poker, in order to deduce their probability.

A card in a poker deck is characterised by a suit (hearts, diamonds, spades, or clubs) and a value (2, 3, ..., 10, jack, queen, king, ace). The game is played with a full deck, which is the Cartesian product of the set of suits and the set of values:

Cards = Suits × Values = {(s,v) | s ∈ Suits and v ∈ Values}.

We construct these examples in Sage:

```sage
sage: Suits = Set(["Hearts", "Diamonds", "Spades", "Clubs"])
sage: Values = Set([2, 3, 4, 5, 6, 7, 8, 9, 10,
....:               "Jack", "Queen", "King", "Ace"])
sage: Cards = cartesian_product([Values, Suits])
```

There are 4 suits and 13 possible values, and therefore 4 × 13 = 52 cards in the poker deck:

```sage
sage: Suits.cardinality()
4
sage: Values.cardinality()
13
sage: Cards.cardinality()
52
```

Draw a card at random:

```sage
sage: Cards.random_element()
(6, 'Clubs')
```

Draw two cards at random:

```sage
sage: Set([Cards.random_element(), Cards.random_element()])
{(2, 'Hearts'), (4, 'Spades')}
```

Returning to our main topic, we will be considering a simplified version of poker, in which each player directly draws five cards, which form his hand. The cards are all distinct and the order in which they are drawn is irrelevant; a hand is therefore a subset of size 5 of the set of cards. To draw a hand at random, we first construct the set of all possible hands, and then we ask for a randomly chosen element:

```sage
sage: Hands = Subsets(Cards, 5)
sage: Hands.random_element()
{(4, 'Hearts'), (9, 'Diamonds'), (8, 'Spades'),
 (9, 'Clubs'), (7, 'Hearts')}
```

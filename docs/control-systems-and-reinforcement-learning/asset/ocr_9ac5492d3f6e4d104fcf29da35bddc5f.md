156

ODE Methods for Algorithm Design

# ## 4.11.2 Optimization

Luenberger has been my favorite source for teaching optimization [230, 231], but the best encyclopedic treatment is probably [73] together with the recent book [19].

A Version of Theorem 4.9 is found in Polyak [286]. The main assumption (4.27) is a restricted form of a bound introduced by mathematician Łojasiewicz, which is why it is called the Polyak–Łojasiewicz (PL) condition in the optimization literature. The simple proof of Theorem 4.9 is taken from [179] (which contains more insight and many applications).

The conclusions of Proposition 4.11 can be improved with a modified algorithm and a more carefully constructed Lyapunov function [116, 292].

It is worth looking over the field of online optimization with application to control [96, 263]. The goals are similar to those of qSGD and policy gradient algorithms.

# ## 4.11.3 QSA

Section 4.5 was initially conceived as an early introduction to stochastic approximation algorithm design – a topic explored in Chapter 8. Over the course of writing this book, the mission evolved to become a stand-alone toolkit for optimization and control.

Much of Sections 4.5–7 is adapted from [40, 41, 87], which was inspired by the prior results [24, 319]; [393] contains algorithms for gradient-free optimization with constraints. The QSA concept was first introduced in [212, 213] for applications to finance.

The theory of two-scale stochastic approximation enjoys a parallel history with the theory of singular perturbations of differential equations, which has played an important role in control theory and applications [186]. A simple example is the dynamical system described by the following equations:

```
$x_1 = f_1(x_1, x_2),\n x_2 = f_2(x_1, x_2).$
```

It is observed that $\epsilon \ll 1$, so that the dynamics of $x_2$ are much faster than that of $x_1$. Suppose that this is a function of time, with $\epsilon \downarrow 0$ as $t \uparrow$. Assume moreover that there is a continuous function $\phi$ satisfying $f_2(x_1, \phi(x_1)) = 0$ for each $x_1$. Under further conditions, there is a tight approximation preceding the preceding ODE and

```
$x_1 = f_1(x_1, \phi(x_1)).$
```

This is the thinking behind Zap QSA (4.91).

PJR averaging was introduced independently by their namesakes [287, 288, 306] (note that Polyak had independent contributions prior to his collaboration with Juditskiy). This work has nothing to do with QSA, but concerns pertaining optimizing the covariance $\Sigma\theta$ appearing in (6.40) for stochastic approximation – see the “Notes” section of Chapter 8 for more background. The application of averaging techniques for real optimization in QSA appears to be new.

The gradient $\hat{g}$ in Lemma 4.37 (1) is precisely the solution to Poisson’s equation, with forcing $\hat{g} = g - a_0$, that appears in simulation of Markov processes, average-cost optimal control, and stochastic approximation [12, 39, 144, 250].

The phrase ODE method is frequently attributed to Ljung [229], though most authors use this to mean a method of analysis rather than a technique for algorithm design. Polyak in
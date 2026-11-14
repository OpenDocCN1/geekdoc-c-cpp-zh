```
\dot{x}_1 = \sigma(x_2 - x_1)
\dot{x}_2 = Rx_1 - x_2 - x_1x_3 \quad (7.5)
\dot{x}_3 = x_1x_2 - bx_3,
```

where \(\sigma, R, b \in \mathbb{R}\) are parameters of the system. Figure 7-1 depicts a trajectory of this system for the typical choice of parameters \(\sigma = 10, R = 28\), and \(b = 10/3\). For these parameter values the Lorenz system exhibits a so-called _Chaotic Attractor_, which can be recognized in Figure 7-1.

Although such a solution is impossible to find analytically, there are mathematical proofs regarding its _existence_ and _uniqueness_ under some conditions on the RHS \(\vec{f}\), e.g., the Picard-Lindelöf theorem, which requires \(\vec{f}\) to be Lipschitz-continuous [68]. Provided that this condition is fulfilled and a unique solution exists—as is the case for almost all practical problems—we can apply an algorithmic routine to find a numerical approximation of this solution.

# ## 7.1.2 Runge-Kutta Algorithms

The most common general-purpose schemes for solving initial value problems of ordinary differential equations are the so-called _Runge-Kutta_ (RK) methods [28]. We will focus on the _explicit_ RK schemes as those are easier to implement and well suited for GPUs. They are a family of iterative one-step methods that rely on a temporal discretization to compute an approximate solution of the IVP. Temporal discretization means that the approximate solution is evaluated at time points \(t_n\). So we use \(\vec{x}_n\) for the numerical approximation of the solution \(x(t_n)\) at time \(t_n\). In the simplest but most frequently used case of an equidistant discretization with a constant step size \(\Delta t\), one writes for the numerical solution:
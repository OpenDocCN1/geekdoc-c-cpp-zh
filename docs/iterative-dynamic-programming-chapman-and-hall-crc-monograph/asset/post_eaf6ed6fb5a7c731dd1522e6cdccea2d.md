
where the transition matrix $\Phi(T)$ is given by

$$
\Phi(T) = \exp(A T) = \sum_{i=0}^{\infty} \frac{(A T)^i}{i!}. \tag{1.28}
$$

Eq. (1.27) can be written as

$$
x(T) = \Phi(T) c + \Psi(T) u(0) \tag{1.29}
$$

where we have introduced the $(n \times m)$ matrix

$$
\Psi(T) = \int_0^T \exp[A(T - \lambda)]\, d\lambda \, B = T \sum_{i=0}^{\infty} \frac{(A T)^i}{(i + 1)!} B. \tag{1.30}
$$

Let us now repeat the procedure but integrate from $t = T$ to $t = 2T$ using a constant value of $u(T)$. Since we are integrating again over a time interval of the same length as before, we get

$$
x(2T) = \Phi(T) x(T) + \Psi(T) u(T). \tag{1.31}
$$

Continuing the procedure, we obtain

$$
x[(k + 1)T] = \Phi(T) x(kT) + \Psi(T) u(kT), \quad k = 0, 1, 2, \ldots . \tag{1.32}
$$

The sampling time $T$ is usually dropped to give a simpler looking equation

$$
x(k + 1) = \Phi x(k) + \Psi u(k), \tag{1.33}
$$

which is a special case of a linear difference equation. If the series expansion for $\Phi$ is asymptotic, then the most convenient way of getting the matrices is to take a truncated series of $N + 1$ terms:

$$
\Theta = \sum_{i=0}^{N} \frac{(A T)^i}{(i + 1)!}. \tag{1.34}
$$

Then

$$
\Phi = I + \Theta A T \tag{1.35}
$$

and

$$
\Psi = \Theta B T. \tag{1.36}
$$

Such a procedure with $N = 20$ was used by Luus and Smith [23] to convert a differential equation describing a gas absorber into a difference equation. If the series is not asymptotic, we can always use the identity

$$
\exp(A T) = [\exp(A T / \beta)]^\beta \tag{1.37}
$$

and choose the constant $\beta$ sufficiently large to make the series asymptotic.

## 1.6 The performance index

In most of the book we denote the performance index by $I$. There are times, however, when an augmented form of the performance index is used, and a different letter such as $J$ may be used, or when a profit function is implied, the letter $P$ is sometimes used.

When the model describing the system is a set of algebraic equations, the performance index is an algebraic expression in the form

$$
I = f(x_1, x_2, ..., x_n). \tag{1.38}
$$

When the system is described by differential equations or difference equations, there are different forms that the performance index can take. For example, we may have the performance index

$$
I = \int_0^{t_f} \phi(\mathbf{x}, \mathbf{u}) \, dt, \tag{1.39}
$$

where $t_f$ denotes final time, or we may have a performance index of the form

$$
I = \mathbf{k}^T \mathbf{x}(t_f) = \sum_{i=1}^{n} k_i x_i(t_f). \tag{1.40}
$$

Both of these are equivalent, as we will now show. Suppose we define a new state variable $x_{n+1}$ by the equation

$$
\frac{dx_{n+1}}{dt} = \phi(\mathbf{x}, \mathbf{u}), \quad x_{n+1}(0) = 0. \tag{1.41}
$$

Then the performance index in Eq. (1.39) is equivalent to

$$
I = x_{n+1}(t_f). \tag{1.42}
$$

This is a special form of Eq. (1.40). Therefore, for most of our work, we choose the performance index as an explicit function of the state at the final time in the form

$$
I = \Phi(\mathbf{x}(t_f)), \tag{1.43}
$$

with the understanding that we have the freedom to choose the state variables accordingly. There are situations, however, when the performance index can not be expressed as a function of the final state. Then we have a *nonseparable* performance index that requires special attention. That will be illustrated and discussed in Chapter 13.

## 1.7 Interpretation of results

An important part of optimization is the interpretation of the results. It is realized that the optimal solution is dependent on the mathematical model and the performance index. Therefore, the results of the optimization must be considered with care. If the mathematical model is an inadequate representation of the physical system, the results are not optimal with respect to the application that has been intended. In the same way, the results are dependent on the choice of the performance index. The choice of the final time $t_f$ has a substantial effect on the optimal control policy [14], but it is frequently chosen quite arbitrarily. Only thorough familiarity with the physical system will ensure successful application of optimization.

Another important aspect of optimization is to determine whether a local optimum or a global optimum has been obtained. In a highly nonlinear problem this can be quite a challenge. The best way to assure oneself that a global optimum has been obtained is to cross-check the optimization by using a different optimization procedure. Simply taking different starting conditions may not yield the global optimum if there is a very large number of local optima. This was recently pointed out in [19] in the optimization of a bifunctional catalyst blend along a tubular reactor to maximize the yield of a desired product. Although 100 different starting conditions chosen at random were used with sequential quadratic programming (SQP), the global optimum was not obtained with that well-established optimization procedure. With iterative dynamic programming, however, the global optimum was readily obtained by Luus and Bojkov [17].

When numerical methods are used for optimization of nonlinear systems, some form of iteration is usually used. There is therefore the additional feature that must be considered, namely the convergence of the iterative procedure itself. The iterations may be ended prematurely, or the iterative procedure itself may fail to converge because of the nature of the problem or the parameters chosen. The problem of convergence is very challenging when a large change in the control policy has a very small effect on the performance index, and one is tempted to accept a highly fluctuating control policy as being optimal. Establishing the optimal control policy for low sensitivity problems is difficult [15]. These are some of the aspects of optimization that we wish to explore in later chapters.

## 1.8 Examples of systems for optimal control

### 1.8.1 Linear gas absorber

A linear system that has been widely used for optimal control studies is the six-plate gas absorber that was used for optimal control studies by Lapidus and Luus [11]. The model was used for time-optimal control studies by Bashein [2] and for time sub-optimal control by Bennett and Luus [3]. More recently it has been used for investigation of the viability of iterative dynamic programming by Luus and Smith [23] and for time-optimal control studies by Bojkov and Luus [4]. Here, based on that six-plate gas absorber model, we consider a more general case of an $n$-plate gas absorber controlled by inlet feed stream concentrations (see Figure 1.1).

![Figure 1.1](img/06ae75163df4fdf5e1eec243d497d393_26_0.png)

Figure 1.1: Gas absorber system consisting of $n$ equilibrium stages

A material balance around the $m$th plate of the absorption tower yields

$$
H\frac{dy_m}{dt} + h\frac{dx_m}{dt} = L(x_{m-1} - x_m) + G(y_{m+1} - y_m), \quad m=1,2,\ldots,n, \tag{1.44}
$$

where

- $x_m, y_m$ = composition of liquid and vapor leaving the $m$th plate (kg solute/kg inert),
- $h, H$ = inert liquid and vapor hold-ups on each plate (assumed constant) (kg),
- $L$ = flow rate of inert liquid absorbent (kg/min),
- $G$ = flow rate of inert gas stream (kg/min),
- $t$ = time of operation (min).

Expressing the flow rates in terms of inerts ensures that $L$ and $G$ remain constant from stage to stage, even though the physical flow rates change because of the absorption process. If a linear relationship is assumed between the compositions in the liquid and vapor in every stage

$$
y_m = a x_m, \tag{1.45}
$$

the mass balance equation can be converted to

$$
\frac{dx_m}{dt} = \frac{d}{e}x_{m-1} - \left(\frac{d+1}{e}\right)x_m + \frac{1}{e}x_{m+1}, \quad m = 1,2,\cdots,n \tag{1.46}
$$

where $d = L/Ga$ and $e = (Ha + h)/Ga$. The use of the convenient set of parameters: $a = 0.72$, $L = 40.8\ \text{kg/min}$, $G = 66.7\ \text{kg/min}$, $H = 1.0\ \text{kg}$, and $h = 75\ \text{kg}$ yields the system equations in vector-matrix form

$$
\frac{d\mathbf{x}}{dt} = \mathbf{A}\mathbf{x}(t) + \mathbf{B}\mathbf{u}(t) \tag{1.47}
$$

where $\mathbf{A}$ is a tridiagonal coefficient matrix given by

$$
\mathbf{A} = \operatorname{tridiag}[0.538998 \quad -1.173113 \quad 0.634115] \tag{1.48}
$$

and the $(n \times 2)$ control coefficient matrix $\mathbf{B}$ is given by

$$
\mathbf{B}^T = \begin{bmatrix} 0.538998 & 0 & \cdots & 0 & 0 \\ 0 & 0 & \cdots & 0 & 0.634115 \end{bmatrix}. \tag{1.49}
$$

The initial condition is chosen as

$$
x_i(0) = -0.0307 - \left(\frac{i-1}{n-1}\right)(0.1273 - 0.0307), \quad i = 1,2,\cdots,n. \tag{1.50}
$$

The performance index to be minimized is

$$
I = \int_0^{t_f} (\mathbf{x}^T\mathbf{x} + \mathbf{u}^T\mathbf{u}) \, dt. \tag{1.51}
$$

Two values for the final time have been used recently [16], namely $t_f = 10\ \text{min}$ and $t_f = 50\ \text{min}$. Also, a range for the number of stages from $n = 10$ to $n = 1000$ has been used to examine the increase of computational effort of iterative dynamic programming as the dimensionality of the problem increases.

### 1.8.2 Nonlinear continuous stirred tank reactor

Let us consider the system consisting of a first-order irreversible chemical reaction carried out in a continuous stirred tank reactor (CSTR) as first formulated by Aris and Amundson [1] and used for control studies by Lapidus and Luus [11]. Control of the reactor is achieved by manipulation of the flow-rate of the cooling fluid through

# 9.2 Variable stage-lengths when final time is free

The development of the algorithm for IDP to allow stages to be of varying length was done by Bojkov and Luus [2]. We consider the stage lengths to constitute another control variable and the formulation is quite straightforward. Let us consider the optimal control problem where the state equation is

$$\frac{d\mathbf{x}}{dt} = \mathbf{f}(\mathbf{x}, \mathbf{u}) \tag{9.8}$$

with the initial state $\mathbf{x}(0)$ given. The $(m \times 1)$ control vector is bounded by

$$\alpha_j \le u_j(t) \le \beta_j, \quad j = 1,2,\cdots,m. \tag{9.9}$$

The performance index to be maximized is a scalar function of the state at the final time $t_f$

$$I = \Phi(\mathbf{x}(t_f)) \tag{9.10}$$

where the final time $t_f$ is not specified. Let us divide the time interval into $P$ time stages, each of variable length

$$v(k) = t_k - t_{k-1}, \quad k = 1,2,\cdots,P \tag{9.11}$$

where

$$v(k) \ge 0, \quad k = 1,2,\cdots,P. \tag{9.12}$$

The control is kept constant in each of these time intervals. Let us now introduce a normalized time variable $\tau$, by defining $d\tau$ in the time interval $t_{k-1} \le t < t_k$ through the relationship

$$dt = v(k)P d\tau \tag{9.13}$$

so that

$$t_k - t_{k-1} = v(k)P(\tau_k - \tau_{k-1}). \tag{9.14}$$

Therefore

$$\tau_k - \tau_{k-1} = \frac{1}{P} \tag{9.15}$$

and in the normalized time the stages are of equal length and the final time is $\tau = 1$, so that the algorithm for IDP presented earlier can be used directly. The only change to be made is that the differential equation now becomes

$$\frac{d\mathbf{x}}{d\tau} = v(k)P\mathbf{f}(\mathbf{x}, \mathbf{u}) \tag{9.16}$$

in the $k$th time interval.
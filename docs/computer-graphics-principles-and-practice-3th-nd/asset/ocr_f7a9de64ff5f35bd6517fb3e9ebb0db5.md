contact: For collisions, objects must overlap along all axes (e.g., at noon on the equator you and the sun have the same $x$-position in your local reference frame, but are separated by a huge vertical distance, so you aren’t inside the sun); and for contact force, we need the normal components from all axes to compute the force along each one. For the moment we ignore contact.

**Velocity** is change in position divided by change in time. When we say “velocity” we typically are referring to **instantaneous velocity** $\dot{x}(t)$, which is the limit of velocity as the time duration approaches zero:

$$\text{velocity}=\dot{x}(t)=\lim_{\Delta t\to 0}\frac{x(t+\Delta t/2)-x(t-\Delta t/2)}{\Delta t}. \tag{35.16}$$

**Acceleration** has the same relationship to velocity as velocity has to position. Instantaneous acceleration can therefore be expressed as the second time derivative of position:

$$\text{acceleration}=\ddot{x}(t)=\lim_{\Delta t\to 0}\frac{\dot{x}(t+\Delta t/2)-\dot{x}(t-\Delta t/2)}{\Delta t}. \tag{35.17}$$

In this notation, our problem is thus to derive an expression for $x(t)$ given $\mathbf{x}(0)$, $\dot{\mathbf{x}}(0)$, and $\ddot{\mathbf{x}}(t)$. By the second fundamental theorem of calculus, if $x(t)$ is differentiable, then

$$\mathbf{x}(t)=\mathbf{x}(0)+\int_0^t\dot{\mathbf{x}}(s)\,ds. \tag{35.18}$$

Since we have the first and second derivatives of $x(t)$, we will assume that it is in fact a differentiable function.

We cannot apply Equation 35.18 directly because we have no explicit expression for $\dot{x}(t)$ in our initial state. Therefore, we apply the second fundamental theorem again to obtain an expression in terms of only known values:

$$\dot{\mathbf{x}}(s)=\dot{\mathbf{x}}(0)+\int_0^s\ddot{\mathbf{x}}(r)\,dr \tag{35.19}$$

$$\mathbf{x}(t)=\mathbf{x}(0)+\int_0^t\left(\dot{\mathbf{x}}(0)+\int_0^s\ddot{\mathbf{x}}(r)\,dr\right)ds \tag{35.20}$$

$$\mathbf{x}(t)=\mathbf{x}(0)+\dot{\mathbf{x}}(0)t+\int_0^t\int_0^s\ddot{\mathbf{x}}(r)\,dr\,ds \tag{35.21}$$

One way to produce a dynamics animation is to evaluate this integral for $x(t)$ analytically and then evaluate it at successive times $t=\{0,\Delta t,2\Delta t,\ldots\}$. When an expression is available for $\ddot{x}(t)$ and it is integrable in elementary (symbolic) terms, this approach is convenient and produces no incremental position error throughout the animation. The analytic approach is viable for simple scenarios, such as a body falling or sliding under constant linear acceleration or a satellite orbiting a planet under constant radial acceleration (both examples due to gravity). Introductory physics textbooks focus on such problems because most complicated scenarios cannot be solved analytically.

# 35.6.2 Differential Equation Formulation

Often we have the means to compute instantaneous acceleration given the position and velocity of an object, but no analytic solution for all time. For example, by Newton’s second law ($F=ma$), the net acceleration $\ddot{x}(t)$ experienced by a body
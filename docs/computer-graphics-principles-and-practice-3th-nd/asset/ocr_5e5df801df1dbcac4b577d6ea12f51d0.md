is the net force applied to it, divided by its mass. The force can often be computed from the current position and velocity of the particle, so given values **x**(t) and **ẋ**(t), we could compute

\[\ddot{\mathbf{x}}(t)=\frac{\mathbf{f}(t,\mathbf{x}(t),\dot{\mathbf{x}}(t))}{m} \tag{35.22}\]

for a particle of known mass m and force function f at any possible time t. (Exceptions arise in situations where the force is controlled by user input, for example.)

Equation 35.22 is a (vector) **differential equation** because it relates **x** and its derivatives. It is specifically an **ordinary differential equation** (ODE) because **x** is a function of a single variable, *t*. Because **f** is arbitrary, this happens to be a nonlinear differential equation, which is a hard class to solve. In fact, there is no known analytic solution for general equations of this form.

Introducing an acceleration function does not immediately help us. That's because we started with the problem that we didn't have analytic solutions for **x** and **ẋ** for all time. Introducing a new function that depends on the two functions we don't know (and which can't be evaluated analytically) seems like we're going in the wrong direction. The key idea here is that if we had values of the functions at a single time, we could compute the forces and thus the acceleration that will help advance the simulation toward a future time without explicitly knowing exactly where it is headed. This will lead us to a numeric integration strategy. This is an important point that underlies most dynamics algorithms. Let us consider a concrete example.

Consider a 1D system of a single falling ball whose height is given by height **x**(t) relative to the ground. Following the notation introduced in Chapter 7, we can explicitly give the type of this function:

\[\mathbf{x}:\mathbb{R}\to\mathbb{R}:t\mapsto\mathbf{x}(t) \tag{35.23}\]

(which we might implement in C as `float x(float t);` but again, this is a function that we'll assume we don't actually have an explicit implementation for).

Likewise, the force function **f** is

\[\mathbf{f}:\mathbb{R}^3\to\mathbb{R}:(t,y,v)\mapsto\mathbf{f}(t,y,v) \tag{35.24}\]

(which we might implement in C as `float f(float t, float y, float v);` and for which we *are* assuming the implementation exists).

The function **f** computes the force on a ball at time *t* if the ball currently has height *y* and velocity *v*. We might model this force as gravity on the Earth's surface:

\[\mathbf{f}(t,y,v) = -9.81\ \mathrm{kg}\cdot\mathrm{m}/\mathrm{s}^2. \tag{35.25}\]

Note that under this model **f** is constant. It doesn't depend on time, position, or velocity.

A more realistic model accounts for the fact that as the ball moves faster, it experiences more friction with the surrounding air. This drag force inhibits the ball's motion. That is, it decelerates the ball along the velocity vector. Choosing an arbitrary drag coefficient, we might enhance our model to

\[\mathbf{f}(t,y,v) = -9.81\ \mathrm{kg}\cdot\mathrm{m}/\mathrm{s}^2 - v\cdot0.5\ \mathrm{kg}/\mathrm{s}. \tag{35.26}\]
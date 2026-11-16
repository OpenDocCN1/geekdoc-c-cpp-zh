# 6.4 Edge-Preserving Smoothing Using the Diffusion Equation

In this section you will learn the relationship between diffusion and blurring, what a Green’s function is, and how to use variable-conductance diffusion to do edge-preserving smoothing of an image.

# 6.4.1 The Diffusion Equation in One Dimension

In one dimension, the “diffusion equation” or “heat equation” is the partial differential equation (PDE),

$$
\frac{\partial f(x,t)}{\partial t} = \frac{\partial}{\partial x} \left[ c \frac{\partial f(x,t)}{\partial x} \right] (6.5)
$$

where c is a scalar known as “conductance.” This equation models the distribution of heat in a material over time.

Think about Eq. 6.5. Both sides are functions of time, and the left-hand side is the rate of change with respect to time. In that equation, we use the notation of differential calculus. Such notation is compact, general, and relatively easy to use when we need to understand the properties of systems or processes. Ultimately, however, we will implement them on a digital computer, which performs operations that are discrete in time and space. Therefore partial derivatives cannot be truly computed, but rather must be estimated, using some discrete estimator such as:

$$
\frac{\partial f(x,t)}{\partial t} \approx f(x,t) - f(x,t-1).
$$

Given an initial function f(x, t0), some estimator, like the right-hand side of Eq. 6.5, can provide an estimate of the time change. Since that is the change with respect to time, it is added to the current estimate,

$$
f(x, t_1) = f(x, t_0) + \Delta_t f(x, t_0).
$$

If a diffusion is run for a time, t, the function f(x, t) becomes more and more blurred as t grows larger. This blurring will be exactly the same as what you would find if the starting image were convolved with a Gaussian kernel with a \(\sigma\) that is a particular function of t.

This relationship between running a PDE over time and the existence of a convolution that does the same thing is the definition of a Green’s function. That is: Suppose we have a PDE that, when run on an image f with a particular set of initial and boundary conditions, produces a result g. If there exists a kernel that, when convolved with f, also produces g, we say the kernel is the “Green’s function” of the PDE. In the case we are describing, convolution with a Gaussian produces the same result as running the diffusion equation (except, of course, for the difference between discrete convolution (a sum of products) and continuous convolution (an integral of a product). Therefore, we say the Gaussian is the Green’s function of the diffusion equation.

Therefore, one can simulate the PDE or one can convolve. The simulation of the PDE as t goes from 0 to T is equivalent to convolution with a Gaussian with \(\sigma\) of

$$
\sigma = \sqrt{2cT} . (6.6)
$$
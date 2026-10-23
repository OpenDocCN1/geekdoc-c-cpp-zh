# ## 26.2 WHAT IS A RANDOM NUMBER GENERATOR?

We give an introduction to a number of methods to generate random numbers. It is useful to give some mathematical background to the C++ code that we introduce.

# ### 26.2.1 Uniform Random Number Generation

Our starting point is the generation of numbers having a *uniform distribution*. To this end, let us suppose that $X$ is a continuous random variable assuming all values in the closed interval $[a,b]$, where $a$ and $b$ are finite. If the *probability density function* (pdf) of $X$ is given by:

$$f(x)=\begin{cases}\dfrac{1}{b-a}, & a\le x\le b\\0, & \text{otherwise}\end{cases} \tag{26.1}$$

then we say that $X$ is *uniformly distributed* over the interval $[a,b]$. A shorthand notation is to say that $X$ is $U(a,b)$. We generate uniformly distributed random numbers by using an algorithm that has been programmed in C or C++.

We now introduce two methods that were popular a number of years ago. We include them here for historical reasons. We also introduce them in the context of the numerical solution of stochastic differential equations (SDEs) in Chapters 31 and 32.

# ### 26.2.2 Polar Marsaglia Method

This method uses the fact that if the random variable $U$ is $U(0,1)$ then the random variable $V$ defined by $V=2U-1$ is $U(-1,1)$. We now choose two variables defined by:

$$V_j=2U_j-1 \quad \text{where}\quad U_j\sim U(0,1),\quad j=1,2.$$

Then we define:

$$W=V_1^2+V_2^2\le 1,\quad W\sim U(0,1).$$

We keep trying with different values until this inequality is satisfied, in other words until $W>0.0$ and $W^2\le 1$. Continuing, we define the intermediate value:

$$Y=\sqrt{-2\log(W)/W}.$$

Finally, the pair of values defined by:

$$N_j=V_jY,\quad j=1,2 \tag{26.2}$$

constitutes two standard normally (Gaussian) distributed random variables.
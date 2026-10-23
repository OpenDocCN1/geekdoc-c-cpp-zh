
```cpp
// Create basic structure for plain options
Lattice<double, TYPEB> lattice(N, 0.0); // init
LatticeMechanisms::ForwardInduction<double>(lattice, algorithm, S0);

// 2.
// Price a plain option
double V0 = LatticeMechanisms::BackwardInduction<double>
            (lattice, algorithm, basePayoff);

// 3.
// a. Find lattice index corresponding to t = T1.
// b. Backtrack from that T1 index.

// a. Find index at t = T1
std::size_t indexT1 = static_cast<std::size_t>(T1/dt);

// b.
double CV0 = LatticeMechanisms::BackwardInduction<double>
              (lattice, algorithm, compoundPayoff, indexT1);

return CV0;
}
```

We now take the example from Haug (2007, p. 136) (put-on-call). The input is:

```cpp
// Option data for 'base' option
OptionData opt;

// Haug 2007 page 136
opt.K = 520.0;
opt.T = 0.5;
opt.r = 0.08;
opt.q = 0.03;
opt.sig = 0.35;
double S0 = 500.0;
std::size_t N = 13000;

// Payoff as a lambda function
double K2 = opt.K;
auto baseCallPayoff = [&K2] (double S) -> double
  {return std::max<double>(S - K2, 0.0);};

double K1 = 50.0;
auto compoundPutPayoff = [&K1] (double V) -> double
  {return std::max<double>(K1 - V, 0.0);};
double T1 = 0.25;

double compoundOptionValue = CompoundOption
            (compoundPutPayoff, T1, // Compound option
```

```
baseCallPayoff, opt,       // Equity option
N,                          // Lattice size
S0);                        // Underlying value
```

The answer that we get is 21.1959.

Answer the following questions:

+   a) Price this problem for the call-on-call option based on the following data (Mun, 2002, p. 187):

```
opt.K = 900.0; // Mun 2002 page 187
opt.T = 3.0;
opt.r = 0.077;
opt.q = 0.0;
opt.sig = 0.30;
double S0 = 1000.0;
double K1 = 500.0;
```

The answer that we get is 165.174.

+   b) Modify the code of the function `CompoundOption()` to include other forward induction algorithms besides the **Tian method** (as discussed in Chapters 11 and 12). Test the schemes.

# 9. (Compound Options, PDE Approach)

The objective of this exercise is to price compound options using the finite difference method. We have already explained the background in Exercise 8. The base and compound option payoff PDEs have already been defined by equations (25.33), (25.34) and (25.35).

Answer the following:

+   a) Write the system (25.33), (25.34) and (25.35) as initial boundary value problems, as in Chapters 20 to 23.

+   b) Create a software framework for this problem using the MOL. You need to take care of the computed discrete payoff of the base option. Compare the results those produced in Exercise 8.

+   c) Solve system (25.33), (25.34) and (25.35) using the ADE method.

# 10. (Chooser Options)

A *chooser option* allows the purchaser to decide whether a derivative will be a European call or put option. These option types can be priced using lattice methods as discussed in Mun (2002) and Exercise 8 using the binomial method, but in this exercise we use PDE models. The underlying PDEs for the two underlying options are given by:

$$\frac{\partial V_j}{\partial t}+\frac{1}{2}\sigma^2S^2\frac{\partial^2 V_j}{\partial S^2}+rS\frac{\partial V_j}{\partial S}-rV_j=0,\quad j=1,2$$  (25.36)

having strike levels $K_1$ and $K_2$, respectively (this is called a *complex chooser option*). The chooser option has the PDE:

$$\frac{\partial C_h}{\partial t}+\frac{1}{2}\sigma^2S^2\frac{\partial^2 C_h}{\partial S^2}+rS\frac{\partial C_h}{\partial S}-rC_h=0$$  (25.37)

with payoff defined by:

$$C_h(S,T_2)=\max\left(V_1(S,T_2)-K_1,\ V_2(S,T_2)-K_2,\ 0\right). \tag{25.38}$$

Answer the following questions:

+   a) Solve this system using the MOL. Test the code using the following data (Haug, 2007, p. 130) using underscores for calls and put:
+   
+   $$S=50$$
+   $$K_c=55;\ K_p=48$$
+   $$T_c=0.5;\ T_p=0.5833$$
+   $$T=0.25\ \text{(chooser)}$$
+   $$r=0.1;\ b=0.1-0.05;\ \sigma=0.35.$$

+   b) The price of a *complex chooser option* has an analytic solution that can be written in terms of the bivariate cumulative normal distribution (Haug, 2007; Mun, 2002; Rubinstein, 1991) that we discussed in Chapter 16. Implement this formula and compare the results with those produced in part a).

+   c) A *simple chooser option* gives the holder the right to choose whether an option is to be a standard call or put after a time $t_1$ with strike $K$ and time to maturity $T_2$ ($t_1<T_2$). Implement the formula as in Haug (2007) and Rubinstein (1991).

# 11. (Viscous Burgers’ Equation)

In this exercise we examine the viscous Burgers’ equation that we introduced in Exercise 21.4. It is a nonlinear wave equation with diffusion added. It models fluid flow and is a simple nonlinear scheme for numerical experiments.

The objective of this exercise is to apply the MOL to this problem. Compare the results with those based on the ADE method.

## 26.2 WHAT IS A RANDOM NUMBER GENERATOR?

We give an introduction to a number of methods to generate random numbers. It is useful to give some mathematical background to the C++ code that we introduce.

### 26.2.1 Uniform Random Number Generation

Our starting point is the generation of numbers having a *uniform distribution*. To this end, let us suppose that $X$ is a continuous random variable assuming all values in the closed interval $[a,b]$, where $a$ and $b$ are finite. If the *probability density function* (pdf) of $X$ is given by:

$$f(x)=\begin{cases}\dfrac{1}{b-a}, & a\le x\le b\\0, & \text{otherwise}\end{cases} \tag{26.1}$$

then we say that $X$ is *uniformly distributed* over the interval $[a,b]$. A shorthand notation is to say that $X$ is $U(a,b)$. We generate uniformly distributed random numbers by using an algorithm that has been programmed in C or C++.

We now introduce two methods that were popular a number of years ago. We include them here for historical reasons. We also introduce them in the context of the numerical solution of stochastic differential equations (SDEs) in Chapters 31 and 32.

### 26.2.2 Polar Marsaglia Method

This method uses the fact that if the random variable $U$ is $U(0,1)$ then the random variable $V$ defined by $V=2U-1$ is $U(-1,1)$. We now choose two variables defined by:

$$V_j=2U_j-1 \quad \text{where}\quad U_j\sim U(0,1),\quad j=1,2.$$

Then we define:

$$W=V_1^2+V_2^2\le 1,\quad W\sim U(0,1).$$

We keep trying with different values until this inequality is satisfied, in other words until $W>0.0$ and $W^2\le 1$. Continuing, we define the intermediate value:

$$Y=\sqrt{-2\log(W)/W}.$$

Finally, the pair of values defined by:

$$N_j=V_jY,\quad j=1,2 \tag{26.2}$$

constitutes two standard normally (Gaussian) distributed random variables.

generate random variables. Let X be a random variable with cumulative probability distribution function F_X(x). Since F_X(x) is a non-decreasing function, the inverse function F_X^{-1}(y) is defined for any value between 0 and 1:

F_X^{-1}(y) = inf {x : F_X(x) ≥ y},      0 ≤ y ≤ 1.

In this case the variable y is given.

In order to create a random variate from a given distribution, let U be uniformly distributed on (0, 1). Then:

X = F_X^{-1}(U) (26.6)

is a random variate of the given distribution.

In general, we need to use numerical methods (for example, the Newton–Raphson method or fixed-point iteration) to compute the random variate X in equation (26.6). In special cases it may be possible to give an analytical solution, but this is more the exception than the rule. For completeness, we give some examples.

# 26.3.1 Analytical Solutions for Random Variate Computations

We examine the one-dimensional uniform distribution on the interval (a, b) whose pdf is given by:

f_X(x) = { 1/(b - a),  a < x < b ; 0, otherwise } (26.7)

and the corresponding cdf is:

F_X(x) = ∫_0^x f_X(y) dy = { 0, x < a ; (x - a)/(b - a), a ≤ x < b ; 1, x ≥ b. } (26.8)

Then, the random variate from the uniform distribution on the interval (a, b) is given by the equation:

X = F_X^{-1}(U) = a + (b - a)U. (26.9)

An exponential variate X with parameter β > 0 has the density (pdf):

f(x) = f_X(x) = { (1/β) e^{-x/β}, 0 ≤ x < ∞, β > 0 ; 0, otherwise } (26.10)

and is denoted by exp(β).


We need to provide the following input describing the initial guess, the function and its gradient:

```
namespace Schaum329
{ // Objective function + gradient; solution is x = .935, y = .998

double minV = 0.8;
double maxV = 0.4;

u::vector<double> Seed()
{
    u::vector<double> result(2);

    result[0] = 0.5;
    result[1] = 0.5;

    return result;
}

double MyFunction(const u::vector<double>& a)
{ // Objective function in NL minimax solvers

double x = a[0]; double y = a[1];
double sp = std::sin(x+y); double cm = std::cos(x-y);

double f = (x-sp);
double g = (y-cm);

    return f*f + g*g;
}

u::vector<double>MyGradient(const u::vector<double>& a)
{ // Gradient function in NL minimax solvers

double x = a[0]; double y = a[1];
double sp = std::sin(x+y); double cm = std::cos(x-y);
double sm = std::sin(x-y); double cp = std::cos(x+y);

u::vector<double>result(2);
double fx = 1.0 - cp;
double gx = sm;
double fy = cp;
double gy = 1.0 - sm;

double f = 2.0*(x-sp);
double g = 2.0*(y-cm);
result[0] = f*fx + g*gx;
result[1] = f*fy + g*gy;

    return result;
}

} // End of namespace
```

A test program and its output is:

```
using namespace Schaum329;                // Checked

u::vector<double>Xk(Seed());             // Copy seed
u::vector<double>XkP1(Xk.size());

// Local bracket
double minBrent = -3.0;
double maxBrent = 3.0;

double TOL = 1.0e-9;
SteepestDescent sa
    (MyFunction, MyGradient, Xk, TOL, minBrent, maxBrent);

sa.run();

std::cout << sa.result() << ", "
    << MyFunction(sa.result()) <<std::endl;
sa.Statistics();
```

```
**** Steepest descent statistics ****

*TOL and [min, max] for Brent: 1e-09, [-3, 3]
*Error and number of iterations needed: 3.08748e-10, 15

(1,0.511685) (2,0.322599) (3,0.067237) (4,0.02977) (5,0.000885976)
(6,0.000644228) (7,5.4778e-05) (8,2.09649e-05) (9,5.78459e-06) (10,4.73895e-07) (11,3.47721e-07) (12,1.66439e-08) (13,9.4501e-09) (14,1.6198e-09) (15,3.08748e-10)

Initial guess: [2] (0.5,0.5)
Final result: [2] (0.935082,0.99802)
Function value: 3.58129e-20
```

You can apply this approach to other problems.

## A2.8.3 What’s Next?

We have discussed unconstrained univariate and multivariate derivative-based optimisation. In many cases we need to solve constrained optimisation problems as seen in equations (A2.19) to (A2.24). A discussion is outside the scope of this book. Furthermore, the steepest descent method has a number of issues that should be addressed:

- 1. It may not always converge if the initial guess is not in a neighbourhood of the exact solution.
- 2. A solution does not always converge to a *global minimum*; in many cases it converges to a *local minimum*.
- 3. We need to calculate the gradient, either analytically or numerically.

- 4. For some methods we may need to compute the Jacobian and Hessian, thereby introducing new numerical challenges.
- 5. These methods are difficult to parallelise.
- 6. Slow convergence.

There are many algorithms that address these problems, one of which is called *Differential Evolution* (DE) (see Price, Storn and Lampinen, 1996). This method does not need an accurate seed, it does not use derivatives and it can be parallelised. We hope to discuss DE and some of its applications in a later work. Incidentally, we have found DE in combination with a least-squares approach to be the most robust method for computing implied volatility.

## A2.9 SUMMARY AND CONCLUSIONS

In this appendix we expanded on the topics introduced in Chapter 19. In particular, we discussed design and code details to make the mathematical content and design approach more tractable. We take the example of computing implied volatility using a variety of methods. We extended the discussion to multivariate optimisation using the *steepest descent* method. Finally, we gave an introduction to simulating mathematical functions and operations using C++.

## A2.10 EXERCISES AND PROJECTS

- 1. *(Implementing Context Diagram 19.1)*
  
  This exercise examines the design and code in Sections A2.2 and A2.3.
  
  a) Run the solvers from Sections A2.2 and A2.3 for the following changes to option data:

```
// sig = 0.25, K = 60
value_type putMarketPrice = 2.4042'3949'490;
value_type callMarketPrice = 3.5923'1909'650;
```

Experiment with different instances of the classes in Figure 19.1.

- b) Stress tests: experiment with ATM, ITM and OTM options. For which range of values do the numerical formulae work?
  
- c) Describe in your own words the advantages of the design approach taken in Section 19.7, in particular, black-box interface specification and how it adds to the readability, maintainability and efficiency of the code.
  
- d) Run the code in parallel as already discussed in this book, for example using C++ threads and tasks.
  
- e) How sensitive are the Banach fixed-point and Aitken algorithms to the choice of initial guess (seed)? In the former case, convergence is assured for any starting value but what can be said of the latter method?
  
- f) Consider making the code for the Banach fixed-point and Aitken algorithms more robust, for example stopping if convergence has not been met within a certain number of iterations or when the denominator in the Aitken algorithm becomes very small.

- 2. *(Computing Square Roots)*
  
  Use the Banach fixed-point theorem to find the solutions of the following nonlinear equations:
  
  a) $x^2 = 2,\quad x_{n+1}=\frac{1}{2}\left(x_n+\frac{2}{x_n}\right),\quad n\ge 0,\quad x_0=1.$

Can you motivate how we arrived at this iteration?

b) x = sin(x + y)
y = cos(x − y)
x₀ = y₀ = 0.5.
Now use the Aitken algorithm to accelerate convergence.

# 3. (Fixed Points and Polynomials)

We solve the equation x = f(x) by the recursion xₙ = f(xₙ₋₁), n ≥ 0, for a given x₀. The recursion converges to a root if: |f′(x)| ≤ L < 1 and the error eₙ is given by eₙ ∼ f′(r)eₙ₋₁.
Apply this method to solving the equation:

F(x) = x³ + 2x² + 10x − 20 = 0

by writing it in the form:

x = 20/(x² + 2x + 10)

(the approximate solution is x = 1.368808107 and it was originally calculated by Leonardo of Pisa (Fibonacci) in 1225).

# 4. (Homotopy and ODEs)

The questions in this exercise refer to Section A2.4:

- a) Generalise the code so that the class Davidenko can be used with any call or put option.
- b) Test the software in the same way as in Exercise 1.
- c) Investigate the relative accuracy of the following steppers:

```
// Bode::runge_kutta4<state_type, value_type> myStepper;
// Bode::runge_kutta_dopri5<state_type, value_type> myStepper;
// Bode::euler<state_type, value_type> myStepper;
// Bode::bulirsch_stoer<state_type, value_type> myStepper;
// Bode::runge_kutta4<state_type, value_type> myStepper;
// Bode::modified_midpoint<state_type, value_type> myStepper;
```

d) Write an observer class to store the solution’s intermediate values and corresponding mesh points by modifying the following class and using it in the ODE solver:

```
class WriteOutput
{ // User-defined observer

public:

public:
    WriteOutput() { }

    void operator()(const state_type &x ,const value_type t)
    {
        // TBD
    }
};
```

# 5. (Yield Computation, Project)

The goal of this *medium-sized project* is to apply the methods of Chapter 19 and this appendix to computing yield. It is recommended because of the hands-on experience of numerical analysis that you will gain.

We test the bisection and Newton methods from the Boost library on a problem from a fixed-income application. In this case we calculate the yield measure of a bond and hence its relative attractiveness. The yield in this case is the interest rate that will make the present value of the cash flows from the investment equal to the price (or cost) of the investment. The yield y satisfies the equation:

$$P = \sum_{t=1}^{n} \frac{CF_t}{(1+y)^t} \tag{A2.30}$$

where:

$P$ = present value  
$CF_t$ = cash flow in year $t$  
$n$ = number of years.

We write this in the form that is suitable for computation:

$$f(y) = P - \sum_{t=1}^{n} \frac{CF_t}{(1+y)^t} = 0. \tag{A2.31}$$

We now have a function of the unknown variable y and in fact we wish to find a root of equation (A2.31).

- Answer the following questions:
  
  **a)** The interval $(a,b)$ in which the solution is to be found must be known.
  
  **b)** In the case of the bisection method we must have $f(a)f(b) < 0$; the values $a = 0$ (zero interest rate) and $b = 0.25$ (25% interest rate) might be good choices but you may have to experiment with some sample values.
  
  **c)** In the case of Newton’s method we need to calculate the derivative of $f$ with respect to $y$, that is:

$$\frac{df}{dy} = \sum_{t=1}^{n} \frac{tCF_t}{(1+y)^{t+1}}. \tag{A2.32}$$

- **d)** A common challenge when employing the Newton method is the choice of initial guess (seed). If it is far from the exact solution then the method will fail to converge, as we have discovered in an MBS application based on the Black, Derman and Toy (BDT) model for the short rate. Under certain circumstances we found that the Newton method failed to converge. We resolved the problem by first bracketing the solution to an accuracy of let’s say 1/10 using the bisection method to find a rough approximation that is then used as a seed for the Newton method.
  
- **e)** Apply this hybrid approach to the current problem. Is this method more robust or more efficient than the bisection and Newton methods?

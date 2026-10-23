
- b) Compare the solutions in part a) with the exact solution (13.15) and the solution produced by the Crank–Nicolson method.
- c) Display the four results from parts a) and b) as four curves in a single Excel sheet. Compare the results.
- d) Experiment with various initial conditions in equation (13.14) and repeat steps a), b) and c).

## 3. (Cubic Spline Overshoots, Part II)

In Chapter 13 we gave a detailed introduction to cubic splines and some of their applications. In particular, Exercise 5 in Chapter 13 was concerned with a discussion on using cubic splines and possible overshoots that can occur with yield curve data. Answer the following questions:

- a) Use the same data as in Exercise 5, Chapter 13 and display the interpolated cubic spline values in Excel.
- b) Compare the results with those produced by linear interpolation (see equation (13.32)).
- c) Display the first and second derivatives of the cubic spline from part a) based on the formulae (13.38) and (13.37), respectively.

## 4. (The Cox–Ingersoll–Ross (CIR) Model)

We examine the CIR interest-rate model (also known as square-root diffusion) defined as the following SDE with constant coefficients (Glasserman, 2004):

dr = a(b − r)dt + σ√r dW.

This is a model of the short rate and it is referred to as the CIR model. In this case the short rate r(t) is pulled towards b at a speed controlled by a. Furthermore, if r(0) > 0 then r(t) will never be negative and r(t) remains strictly positive for all t if the following Feller condition is satisfied:

ab > ½ σ².

The objective of this exercise is to introduce this model into the framework in Figure 14.6 and gain an insight into its analytical and numerical properties.

Answer the following questions:

- a) Create a class for the CIR SDE and integrate it into the framework.
- b) The CIR SDE does not have an explicit solution. We then resort to numerical methods. Apply the explicit Euler and Heun methods for various time-step sizes and expirations.
- c) Investigate the finite difference schemes when the Feller condition is not satisfied.
- d) Experiment with the finite difference schemes and determine positivity for small and large values of drift, volatility and expiration parameters.

We remark that the transition density for the CIR process is known and it can be represented in terms of a non-central chi-squared distribution (Glasserman, 2004, p. 122).

## 5. (SDEs with Analytical Solutions)

In some cases (we might get lucky) it is possible to find analytical solutions to SDEs (Kloeden and Platen, 1995, pp. 118–126). Some examples of SDEs and their solutions are:

```text
dX = ½ a² X dt + a X dW
X(t) = X₀ exp(aW(t))

dX = aX dt + bX dW
X(t) = X₀ exp((a − ½ b²)t + bW(t))

dX = ½ X dt + X dW
X(t) = X₀ exp(W(t))
```

Here W(t) is a Wiener process.

Answer the following questions:

- a) Integrate these equations into the framework and decide how to determine the difference between the explicit solution and the solution defined by a given finite difference scheme.
- b) Experiment with the schemes by varying the number of time steps. Is there some way to determine what the order of convergence of a given scheme is?
- c) We focus on the explicit Euler method. Produce a multi-curve graph in the style of Figure 14.5 in which each curve is a path produced by the Euler method with a given number of time steps, for example step sizes NT = 10, 20, 50, 100, 200, 300. Do you see monotonic convergence to the ‘exact path’ as NT increases?

## 6. (Log–Log and Semi-log Plots)

In some cases we may wish to transform data in some way before presenting it in Excel. In general, the linear plot between the horizontal x and vertical y axes can be transformed in two main ways:

- **Log–log plot:** uses a logarithmic scale for both the horizontal and vertical axes. This transformation is suitable for monomials (relationships of the form y = a x^k). These become straight lines in log space, as the following steps show:

```text
y = a x^k
log y = k log x + log a
X = log x, Y = log y
Y = m X + b.
```

We thus see that m = k is the slope (gradient) of the straight line while b = log a is the intercept on the log y axis, so this graph can recognise relationships and estimate parameters (in this case the parameters a and k).

- **Semi-log plot:** in this case only one of the variables is log transformed. We distinguish between log-lin in which the y axis is transformed and lin-log in which the x axis is transformed. Equations of the form y = λ a^{γ x} become straight lines when plotted semi-logarithmically, as the following steps show:

```text
log y = log(λ a^{γ x}) = log λ + log(a^{γ x}) = log λ + (γ log a) x.
```

In general, any log base can be used but most applications use base 10, 2 or e.

Answer the following questions:

- a) Determine how to introduce log transformations into the current Excel driver framework.
- b) As a test case, we take the example \(y=x^2/2\). Generate \(x\) and \(y\) array values on the interval [1,10]. Then perform a log–log transform on the arrays and plot the arrays in Excel. Can you reproduce or ‘see’ the original parameters from the slope and intercept of the straight line?

## 7. (Extending the Framework in Figure 14.6, Brainstorming)

The solution to this exercise is discussed in Chapter 31 but it does no harm to address the problem as early as possible in the book. The focus is on extending the design in Figure 14.6 to create a small one-factor Monte Carlo option pricer.

Answer the following questions:

- a) Consider the initial case of pricing one-factor call and put option prices. Which new systems and classes need to be added to the framework? A requirement is that the framework should compute option price and the standard error.
- b) The mediator class needs to be extended because in its current form it computes a single path only. Using the Monte Carlo method entails that we create a large number of paths and that we use well-known averaging and discounting algorithms.
- c) Test the code from parts a) and b) for call and put options and compare exact and approximate solutions with each other.
- d) Extend the framework so that it can be configured to simultaneously price several options for the same path information.

## 14.9 APPENDIX: COM ARCHITECTURE OVERVIEW

In this section we give a global overview of the *Component Object Model* (COM). We introduce it because it underpins much of Excel. You may skip Sections 14.9, 14.10 and 14.11 without loss of continuity, although you should read Sections 14.12 and 14.13. The two key entities in COM are *interfaces* and *components*. In this section we explain what they are from a conceptual viewpoint and we then discuss how COM realises them. An *interface* is a pure specification of intended behaviour. In other words, it consists of a set of *abstract methods*. Each method is devoid of implementation and an interface may not contain non-abstract methods nor may it contain member data. This description is consistent with how C# and Java support interfaces. C++ does not support interfaces as such (abstract classes in C++ are not interfaces because they are structural entities), but they can be emulated by classes having no member data and consisting solely of pure virtual functions. COM has a keyword called `interface` that is defined as follows:

```cpp
#define interface struct
```

which is defined in the file `objbase.h` header included in the Microsoft Win32 *Software Development Kit* (SDK). We take an initial example in C++ that emulates COM functionality. To this end, we define two interfaces that contain methods for presenting data in different ways. We then use *multiple inheritance* to create a class that implements both interfaces. The code is:

```cpp
#include <iostream>
#include <objbase.h>              // Define interface.

// Abstract interfaces
interface IDraw
{ // Present information

    virtual void __stdcall display() = 0;
    virtual void __stdcall print() = 0;
};

interface ISave
{ // Save to permanent storage

    virtual void __stdcall saveXML() = 0;
    virtual void __stdcall saveDB() = 0;
};

// Interface implementation
class CA : public IDraw, public ISave
{
public:

    // Implement interface IDraw.
    virtual void __stdcall display()
    {std::cout << "CA::display" << std::endl;}
    virtual void __stdcall print()
    {std::cout << "CA::print" << std::endl;}

    // Implement interface ISave.
    virtual void __stdcall saveXML()
    {std::cout << "CA::saveXML" << std::endl;}
    virtual void __stdcall saveDB()
    {std::cout << "CA::saveDB" << std::endl;}
};
```

We first note that this code is still C++ and not COM code. Second, this code contains the Microsoft-specific extension to the compiler called `__stdcall`. This is a somewhat technical issue and it is concerned with method arguments, how they are pushed onto the stack and who (whether it is the caller or the callee) removes them from the stack. The general options are:

- **cdecl**: arguments are pushed onto the stack in reverse order, that is from right to left and the caller (calling function) cleans up the stack. This is the C language convention.
- **pascal**: arguments are pushed onto the stack from left to right and the callee cleans up the stack. This was the calling convention in the Win16 operating system.
- **stdcall**: this is the standard and most common calling convention. It is a variation of the pascal calling convention and in this case the callee cleans the stack but the parameters are pushed onto the stack from right to left. It is the convention used by the application programming interfaces in the Win32 operating system.

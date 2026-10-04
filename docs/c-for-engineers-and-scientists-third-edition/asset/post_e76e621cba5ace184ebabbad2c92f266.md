
# 752 Numerical Methods

you need to begin solving numerical problems immediately. Besides, root-solving problems can be fun.
The following list shows some examples of the types of functions encountered in root-solving problems:

```
$ax^2 + bx + c = 0$ (Equation 14.1)
$2x^4 - 7x^3 + 4x^2 + 7x - 6 = (x - 2)(x + 1)(2x - 3) = 0$ (Equation 14.2)
$x^5 - 2x^3 + 5x^2 - 2 = 0$ (Equation 14.3)
$\sin(x) + \sin^3(x) + 5\cos(x) - 7 = 0$ (Equation 14.4)
$100e^{-x} - \sin(2\pi x) = 0$ (Equation 14.5)
```

The general quadratic equation, Equation 14.1, can be solved easily and exactly by using this quadratic formula:

```
$r = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$
```

Equation 14.2 can be solved for x exactly by factoring the polynomial. The roots are then clearly 1, -1, 2, and 3/2. However, most polynomials cannot be factored easily, and other general techniques are required. There are formulas for the exact solution of general cubic or quartic equations, but they are cumbersome and, therefore, seldom used. No exact formula is possible for a polynomial such as Equation 14.3, in which the highest power of x is greater than 4. For these polynomials, numerical means must generally be used to determine the roots.

Recall from high school algebra that a polynomial of degree $n$ (that is, the highest power of $x^n$) has precisely $n$ roots, of which some can be complex numbers and others can be multiple roots. Therefore, Equation 14.3 has three real roots

```
$r_1 = -0.7127809844625...$
r_2 = 0.579098844162...
r_3 = 2.0508836199...
```

and two complex roots:

```
$r_4 = 0.775225433526 + i(0.57803468208)$
r_5 = 0.775225433526 - i(0.57803468208)$
```

The equation

```
$x^2 - 2x + 1 = 0$
```

can be factored as

```
$(x - 1)^2 = 0$
```

# Chapter 14: Introduction to Root Finding

and has two real roots, both of which happen to be the same. In this case, the root is said to be a multiple root with multiplicity 2.

Equations 14.4 and 14.5 are called transcendental equations and represent an entirely different class of functions. Typically, transcendental equations involve trigonometric, exponential, or logarithmic functions and cannot be reduced to any polynomial equation in x. The real roots of polynomials are usually classified as rational numbers (a simple fraction) or irrational (for example, $\sqrt{2}$). The roots of transcendental equations are transcendental, such as $\pi$.

Irrational and transcendental numbers are represented by nonrepeating decimals and fractions which are important to mathematics because they are responsible for the number system being dense and continuous. Furthermore, classifying equations as polynomials or transcendental and the roots of these equations as irrational is vital to traditional mathematics; however, the distinction is less consequence to the matter. In fact, the number system is not only continuous, but also a finite set.

At any rate, when finding the distinction between polynomials and transcendental equations is unnecessary, the numerical procedures applied to both. The distinction between the two types of functions is, however, important in other regions. Many of the theorems you learned for roots of polynomials do not apply to transcendental equations. For instance, Equations 14.4 and 14.5 have an infinite number of real roots.

All the root-solving techniques discussed in this chapter are interactive; that is, you specify an interval that contains a root or provide an initial guess for the root, and the various routines return a limited interval or a better guess. Some schemes discussed in this chapter are guaranteed to find a root, albeit arriving at the answer might take considerable computer time. Others converge to a root much faster but are more susceptible to divergence; in other words, they come with no guarantees.

The common ingredient in all root-solving recipes is that potential computational difficulties can be avoided by providing the best choice of a method and the initial guess, based on your knowledge of the function. A good solution is the most difficult and time-consuming. The art of numerical analysis involves balancing spent optimizing the solver's solution against time spent correcting errors during computation.

If possible, you should sketch the function before you attempt root solving; you can use graphing or generate a table of function values that are graphed by hand. These graphs are useful to programmers in estimating the first guess for the root as well as anticipating potential difficulties. If a sketch is infeasible, you must use some method of monitoring the function to understand what the function is before you start the actual computation. As an example of the general procedure to follow, take a look at this transcendental function:

```
$f(x) = e^x - \sin(\pi x)$
```

This equation, as you'll see, has an infinite number of positive roots. For the moment, concentrate on obtaining an initial guess for the first root, and then use this initial guess to find a more precise root value.

Begin by gathering as much information as possible before trying to construct a C++ program. This step almost always involves making a rough sketch of the function. The previous equation can be written as:

$e^x = \sin(\frac{1}{2}\pi x)$

A root of this equation then corresponds to any value of $x$ so that the left side and right side are equal. If the left and right sides are plotted separately, the roots of the original equation are given by the points of intersection of the two curves (see Figure 14.1). From the sketch, you can see that the roots are the following:

Roots $\approx 0.4, 1.9, 4.0, \dots$

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_773_0.png)

Figure 14.1 Graph of $e^x$ and $\sin(\frac{1}{2}\pi x)$ for locating the intersection points

Since the sine oscillates, there are an infinite number of positive roots. First, you should concentrate on improving the estimate of the first root near 0.4. You begin by establishing a procedure, or algorithm, that is based on the most obvious method of attack when using a pocket calculator; that is, begin at some value of $x$ just before the root (say, 0.3) and step along the $x$-axis, carefully watching the magnitude and particularly the sign of, as:

Notice that the function has changed sign between 0.4 and 0.5. For the next approximation, you use the midpoint value, $x = 0.45$, for the next step:

| Step | x | $e^x$ | $\sin(\frac{1}{2}\pi x)$ | $f(x) = e^x - \sin(\frac{1}{2}\pi x)$ |
|---|---|---|---|---|
| 0 | 0.3 | 0.741 | 0.454 | 0.297 |
| 1 | 0.4 | 0.678 | 0.588 | 0.088 |
| 2 | 0.5 | 0.606 | 0.707 | -0.101 |
| 3 | 0.45 | 0.638 | 0.649 | -0.012 |
| 4 | 0.425 | 0.654 | 0.619 | 0.034 |
| 5 | 0.4375 | 0.6456 | 0.6344 | 0.0112 |
| 6 | 0.44365 | 0.6417 | 0.6418 | -0.0001 |

Wait, the table in the OCR seems to have been split or merged. Let me re-align based on logic:

| Step | x | $e^x$ | $\sin(\frac{1}{2}\pi x)$ | $f(x) = e^x - \sin(\frac{1}{2}\pi x)$ |
| --- | --- | --- | --- | --- |
| 0 | 0.3 | 0.741 | 0.454 | 0.297 |
| 1 | 0.4 | 0.678 | 0.588 | 0.088 |
| 2 | 0.5 | 0.606 | 0.707 | -0.101 |
| 3 | 0.45 | 0.638 | 0.649 | -0.012 |
| 4 | 0.425 | 0.654 | 0.619 | 0.034 |
| 5 | 0.4375 | 0.6456 | 0.6344 | 0.0112 |
| 6 | 0.44365 | 0.6417 | 0.6418 | -0.0001 |

Actually, looking at the OCR, the table is fragmented. I will reconstruct it correctly based on the provided fragments.

| Step | x | $e^x$ | $\sin(\frac{1}{2}\pi x)$ | $f(x) = e^x - \sin(\frac{1}{2}\pi x)$ |
|---|---|---|---|---|
| 0 | 0.3 | 0.741 | 0.454 | 0.297 |
| 1 | 0.4 | 0.678 | 0.588 | 0.088 |
| 2 | 0.5 | 0.606 | 0.707 | -0.101 |
| 3 | 0.45 | 0.638 | 0.649 | -0.012 |
| 4 | 0.425 | 0.654 | 0.619 | 0.034 |
| 5 | 0.4375 | 0.6456 | 0.6344 | 0.0112 |
| 6 | 0.44365 | 0.6417 | 0.6418 | -0.0001 |

Wait, the OCR has:
"| 0 | 0.3 | 0.741 | 0.454 | 0.297 |"
"| 1 | 0.4 | 0.678 | 0.588 | 0.088 |"
"| 2 | 0.5 | 0.606 | 0.707 | -0.101 |"
"| 3 | 0.45 | 0.638 | 0.649 | -0.012 |"
"| 4 | 0.425 | 0.654 | 0.619 | 0.034 |"
"| 5 | 0.4375 | 0.6456 | 0.6344 | 0.0112 |"
"| 6 | 0.44365 | 0.6417 | 0.6418 | -0.0001 |"

I will use this reconstructed table.

The function has changed sign between 0.4 and 0.5. For the next approximation, you use the midpoint value, $x = 0.45$, for the next step.

# 14.2 The Bisection Method

The root-solving procedure explained in Section 14.1 is suitable for hand calculations; although a slight modification makes it more systematic and easier to adapt to computer coding. This modified computerized technique is known as the bisection method. If you already know there's a root between x=a and x=b, that is, the function changes sign in this interval. Assume there's only one root between x=a and x=b and the function is continuous in this interval.

The function might then resemble the sketch in Figure 14.2. If you define x₁=a and x₂=b as the left and right ends of the interval, and x₃=½(x₁+x₂) as the midpoint, in which half-interval does the function cross the x-axis? If the crossing is on the right, so you replace the full interval by the right half-interval.

# EXERCISES 14.1

- 1. (Practice) Use the iterative technique presented in this section to find a root of the equation f(x) = sin x - x/3 = 0 (x is in radians)
To do this, first rewrite the equation as
sin x = x/3
plot the left and right sides separately on the same graph.

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_774_0.png)

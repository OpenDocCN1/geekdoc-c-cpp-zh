
> FibonacciSearch(9, 0, 20, 0.1):
> fnormal(%, 5);  # to fit the output to the page width

The maximum is f(2.523088)=1.203630 with tolerance 0.001000

| Iteration | $x_1$ | $x_2$ | $f(x_1)$ | $f(x_2)$ | Interval |
|---:|---:|---:|---:|---:|:---|
| 0.0 | 7.6395 | 12.361 | 1.1153 | 1.0748 | [0.0, 20] |
| 1 | 4.7210 | 7.6395 | 1.1659 | 1.1153 | [0.0, 12.361] |
| 2 | 2.9179 | 4.7210 | 1.2012 | 1.1659 | [0.0, 7.6395] |
| 3 | 1.8032 | 2.9179 | 1.1920 | 1.2012 | [0.0, 4.7210] |
| 4 | 2.9179 | 3.6066 | 1.2012 | 1.1899 | [1.8032, 4.7210] |
| 5 | 2.4920 | 2.9179 | 1.2036 | 1.2012 | [1.8032, 3.6066] |
| 6 | 2.2289 | 2.4920 | 1.2021 | 1.2036 | [1.8032, 2.9179] |
| 7 | 2.4920 | 2.6547 | 1.2036 | 1.2033 | [2.2289, 2.9179] |
| 8 | 2.3916 | 2.4920 | 1.2034 | 1.2036 | [2.2289, 2.6547] |
| 9 | 2.4920 | 2.5542 | 1.2036 | 1.2036 | [2.3916, 2.6547] |
| 10 | 2.4537 | 2.4920 | 1.2036 | 1.2036 | [2.3916, 2.5542] |
| 11 | 2.4920 | 2.5158 | 1.2036 | 1.2036 | [2.4537, 2.5542] |
| 12 | 2.5158 | 2.5304 | 1.2036 | 1.2036 | [2.4920, 2.5542] |

The Fibonacci search gives the maximum as $f(2.5)=1.204$. How does this answer compare with the optimum found by the Golden Section search?

## Interpolation with Derivatives: Newton’s Method

### Finding the Critical Points (Roots of the Derivative of a Function)

Newton’s Method can be adapted to solve nonlinear optimization problems. For a twice differentiable function of one variable, the adaptation is straightforward. Newton’s Method is applied to the derivative, rather than the original function we wish to optimize—the function’s critical points occur at roots of the derivative. Replace $f$ with $f'$ in the iterating formula for Newton’s Method:

$$N(x)=x-\frac{f(x)}{f'(x)} \quad\Rightarrow\quad M(x)=x-\frac{f'(x)}{f''(x)}$$

Given a specified convergence $\varepsilon>0$, the iterations of Newton’s Method can be terminated when $|x_{k+1}-x_k|\leq\varepsilon$ or when $|f'(x_k)|<\varepsilon$.

In order to use the modified Newton’s Method to find critical points, the function’s first and second derivatives must exist throughout the neighborhood of interest. Also note that whenever the second derivative at $x_k$ is zero, the
next point $x_{k+1}$ cannot be computed. (*Explain why?*) This method finds only approximates the value of critical points; it does not know what it is finding a maximum or a minimum of the original function. Use the sign of the second derivative to determine whether the critical value is a maximum, minimum, or neither (a likely inflection point).

## **Example 3.9. A Simple Application.**

Maximize the polynomial $p(x)=5x-x^2$ over the interval $[0,7]$.

This simple problem is easy to solve using elementary calculus.

- 1. Differentiate: $p'=5-2x$.
- 2. The only critical point, the root of $p'$, is $x^*=5/2$.
- 3. Differentiate again: $p''=-2<0$.
- 4. The Second Derivative Test indicates that $p$ has a maximum of $25/4$ at $x^*=5/2$.

Let's use Maple to implement the modified Newton’s method for finding the maximum of $p$.

```
> p := x → 5x − x² :
  dp := D(p) :
  ddp := D(dp) :

> Newton := x → x − dp(x)/ddp(x) :
```

Start with $x_0=1.0$.

```
> x₀ := 1.0 :
  x₁ := Newton(x₀);
  x₂ := Newton(x₁);

                         x[0] := 1.0
                         x[1] := 2.500000000
                         x[2] := 2.500000000
```

Starting at any other value also yields $x^*=2.5$. Since this simple quadratic function has a linear derivative, the linear approximation of the derivative will be exact regardless of the starting point, and the answer will appear at the second iteration. See **Figure 3.6**. Algebraically simplifying the method’s iterating function for $p$ confirms this: $Newton(x)=2.5$.

![](img/0f04050177d82aebd17d3383d7334896_131_0.png)

The slope of the linear approximation of the function at the point is precisely the slope of the function at that point, so the linear approximation is tangent to the function at the point as shown in the figure.

## **Example 3.10. A Third Degree Polynomial.**

Find a maximal point, if possible, for $p(x)=-2x^3+10x+5$ on the interval $[0,3]$ to a tolerance of $\varepsilon=0.01$.

We’ll use the same process in Maple, this time, with the starting value $x=1.0$.

```
> p := x → −2x^3 + 10x + 5:
    dp := D(p):
    ddp := D(dp):

> Newton := x → x − dp(x)/ddp(x):
```

Start again with $x_0=1.0$.

```
> x_0 := 1.0:
    x_1 := Newton(x_0):
    x_2 := Newton(x_1):

                     x[0] := 1.0
                     x[1] := 1.333333333
                     x[2] := 1.291666667

> abs(x[2] − x[1]) < 0.01
                     0.041666666 < 0.01
```

The desired tolerance has not been achieved—we’re not finished.

```
Newton(x₂);
|x₃ − x₂| < 0.01;

x₃ := 1.290994624
0.000672043 < 0.01
```

We have a result! Checking the second derivative shows that p(1.29) = 13.6 is our maximum (to within 0.01).

Maple’s *Student[Calculus1]* package contains *NewtonsMethod* for finding the roots of a function. To use *NewtonsMethod* to find critical points, all we have to do is replace the function with its first derivative. We illustrate below.

```
with(Student[Calculus1]);

p := x → −2x³ + 10x + 5:
dp := D(p):
NewtonsMethod(dp, x = 1.0);

1.290994449

NewtonsMethod(dp, x = 1.0, output = sequence);

1.0, 1.333333333, 1.291666667, 1.290994624, 1.290994449

NewtonsMethod(dp, x = 0.3, output = plot);
```

![](img/0f04050177d82aebd17d3383d7334896_132_0.png)

From the initial point x₀ = 0.3, at most 5 iteration(s) of Newton’s method for f(x) = −6x² + 10

Try *NewtonsMethod* with *output=animation*.

## Exercises

Compare the results of using the Golden Section, Fibonacci’s, and Newton’s methods in the following.

- 1. Maximize \(f(x)=-x^2-2x\) on the closed interval \([-2,1]\). Using a tolerance for the final interval of 0.6. Hint: Start Newton’s method at \(x=-0.5\).
- 2. Maximize \(f(x)=-x^2-3x\) on the closed interval \([-3,1]\). Using a tolerance for the final interval of 0.6. Hint: Start Newton’s method at \(x=1\).
- 3. Minimize \(f(x)=x^2+2x\) on the closed interval \([-3,1]\). Using a tolerance for the final interval of 0.5. Hint: Start Newton’s method at \(x=-3\).
- 4. Minimize \(f(x)=-x+e^x\) over the interval \([-1,3]\) using a tolerance of 0.1. Hint: Start Newton’s method at \(x=-1\).
- 5. List at least two assumptions required by both Golden Section and Fibonacci’s search methods.
- 6. Consider minimizing \(f(x)=-x+e^x\) over the interval \([-1,3]\). Assume the search method yielded a final interval of \([-0.80,0.25]\) to within the tolerance of \(\varepsilon\). Report a single best value of \(x\) to minimize \(f(x)\) over the interval. Explain your reasoning.
- 7. Modify the Golden Section (pg. 109) algorithm to find a minimum value of a unimodal function. Write a Maple procedure to implement your change.
- 8. Modify the Fibonacci search (pg. 113) algorithm to find a minimum value of a unimodal function. Write a Maple procedure to implement your change.

## Projects

- **Project 3.1.** Write a program in Maple that uses a *secant method search*. Apply your program to Exercises 1 through 4 above.
- **Project 3.2.** Write a program in Maple that uses a *Regula-Falsi search* method. Apply your program to Exercises 1 through 4 above.
- **Project 3.3.** Carefully analyze the *rate of convergence* of the different search methods presented.

## References and Further Reading

[BSS2013] Mokhtar S. Bazaraa, Hanif D. Sherali, and Chitharanjan M. Shetty, *Nonlinear Programming: Theory and Algorithms*, Wiley, 2013.

[B2016] William C. Bouldry, *Introduction to Computation*, 2016.

[F1992] William P. Fox, “Teaching nonlinear programming with Minitab,” COED Journal, Vol. II (1992), no. 1, 80–84.

[F1993] William P. Fox, “Using microcomputers in undergraduate nonlinear optimization,” Collegiate Mathematics, Vol. XI (1993), no. 3, 214–218.

[FA2000] William P. Fox and Jeffrey Applegate, “Some fun with Newton’s method,” COED Journal, Vol. X (2000), no. 4, 38–43.

[FGMW1987] William P. Fox, Frank Giordano, S. Maddox, and Maurice D. Wey, *Mathematical Modeling with Minitab*, Brooks/Cole, 1987.

[FR2000] William P. Fox and William Richardson, “Mathematical modeling with least squares using Maple,” Maple Application Center, Nonlinear Mathematics, 2000.

[FGW1997] William P. Fox, Frank Giordano, and Maurice Weir, *A First Course in Mathematical Modeling*, 2nd Ed., Brooks/Cole, 1997.

[FW2001] William P. Fox and Margie Witherspoon, “Single variable optimization when calculus fails: Golden section search methods in nonlinear optimization using Maple,” COED Journal, Vol. XI (2001), no. 2, 50–56.

[GFH2014] Frank Giordano, William P. Fox, and Steven Horton, *A First Course in Mathematical Modeling*, 5th ed., Nelson Education, 2014.

[M2013] Mark M. Meerschaert, *Mathematical Modeling*, Academic Press, 2013.

[PRS1976] D.T. Phillips, A. Ravindran, and J. Solberg, *Operations Research*, Wiley, 1976.

[PFTV2007] William H. Press, Brian P. Flannery, Saul A. Teukolsky, William T. Vetterling, et al., *Numerical Recipes*, Cambridge U. Press, 2007.

[R1979] S.S. Rao, *Optimization: Theory and Applications*, Wiley Eastern Ltd., 1979.

[WVG2003] W.L. Winston, M. Venkataramanan, and J.B. Goldberg, *Introduction to Mathematical Programming*, Duxbury, 2003.

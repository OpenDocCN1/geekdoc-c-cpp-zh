```
f(0)-g(0)=E
f(x)-g(x)=-E
f(1)-g(1)=E
\frac{d}{dx}[f(x)-g(x)]=0.
```

Substituting everything shows us that we are actually dealing with a system of four unknowns with four equations:

```
a+b\cdot 0-3\cdot 0^2 = E
a+bx-3x^2 = -E
a+b\cdot 1-3\cdot 1^2 = E
b-6x = 0.
```

This system can easily be solved by any method we wish to apply. Doing so reveals that the answer to this specific problem is \((a, b) = (-\frac{2}{3}, 3)\). We can also try the same method against any reference function \(g(t)\) to notice how easy it is to compute the minimax approximation for the second level. The maximum error of a minimax approximation is always given by the difference of the original function and the approximation at either of the endpoints of the interval over which the approximation is applied. We can obtain the values for the third degree minimax approximation using the same logic expressed here. Where it becomes tricky is when we want to compute the minimax approximation for polynomials of degree higher than three. We reach a point where we have fewer knowns than unknowns, and we thus cannot solve the system. In these cases, we must resort to more sophisticated mathematical techniques to solve the problem at hand.

# Solving the Minimax Approximations for Arbitrary Degrees

It is by no means trivial to obtain the coefficients of an arbitrary minimax approximation. There are no strict speed requirements in finding the solution because it does not need to be solved in real time. The Remez algorithm can help us solve the problem at hand and goes as follows.

+   1. Choose an initial guess for the coefficient vector c.
+   2. If the error E is satisfactory, stop. Otherwise, find the maximum vector x in \(h(x) = g(x) - f(x)\) given c.
+   3. Find the values for the coefficient vector c (forget about the previous value for c) for the linear system \(g(x) - f(x) = (-1)^i E\), given the maximum vector x, and go back to step 2.
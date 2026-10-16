One simple numerical method for finding an approximate solution of an equation f(x) = 0 is the bisection method. (The programming problems describe another commonly used method known as the Newton-Raphson method.) In the bisection method, we begin with an interval [a, b] where the function values f(a) and f(b) at the endpoints have opposite signs. If f is continuous in this interval—that is, there is no break in the graph of y = f(x) in this interval—then the graph of f must cross the x-axis at least once between x = a and x = b, and thus there must be at least one solution of the equation f(x) = 0 between a and b. To locate one of these solutions, we first bisect the interval [a, b] and determine in which half f changes sign, thereby locating a smaller subinterval containing a solution of the equation. We bisect this subinterval and determine in which half of it f changes sign; this gives a still smaller subinterval containing a solution.

![](bbox=[0.22, 0.31, 0.8, 0.65])

Repeating this process gives a sequence of subintervals, each of which contains a solution of the equation and has a length one-half that of the preceding interval. Note that at each step, the midpoint of a subinterval of length L is within L / 2 of the exact solution:

![](bbox=[0.45, 0.8, 0.62, 0.9])

The program in Example 6.11 uses the bisection method to find an approximate solution of

f(x) = x³ + x − 5 = 0

It generates successive approximations to a solution, terminating when an interval is obtained whose length guarantees a specified accuracy entered by the user.
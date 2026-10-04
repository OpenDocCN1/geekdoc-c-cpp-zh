# Chapter 14

# 783

# 14.8 Common Programming Errors

In the modified bisection root-finding method, two problems can occur. The first problem is round-off error, which can occur when the values of $f(x_i)$ and $f(x_i)$ used in the computation are nearly equal. The second problem occurs when a prediction of the exact number of iterations required to achieve a specific accuracy isn't available. To counter these two problems successfully, the code used in these two methods must detect their occurrence to prevent excessive and possibly infinite iterations.

In numerical integration, excessive computation times can also be a problem. Problem typically occurs when the number of iterations exceeds 50. You can reduce runtime a bit by inspecting each program loop to ensure that only calculations that must be computed iteratively are included in the loop, and moving all other calculations to be computed before or after the loop is completed.

# 14.9 Chapter Summary

The root-solving methods described in this chapter are either iterative or can-based, depending on whether you're starting with a root or an initial estimate of the root. The bisection-based procedures begin with an interval that known to contain a root and are guaranteed to converge within a precise tolerance reaching the root. In the bisection methods, the modified regula falsi is faster and recommended.

In algorithms based on bisection method, the initial interval is refined by evaluating the function repeatedly within the interval, and by monitoring the sign of the function and determining which subinterval lies. If the left and right of the current interval are $x_i$ and $x_j$, respectively, the standard bisection method uses the function evaluated at the midpoint, $x_m = (x_i + x_j)/2$. The sign of the function at $x_i$ is compared with $f(x_i)$ and at either end of the interval to determine which half of the interval contains the root. The full interval is then replaced by that half, and the process is repeated. After $n$ iterations, the root is contained in an interval of size $|x_j - x_i|$.

In the regula falsi method, the conditions are the same as for the bisection method. Instead of using the midpoint, a straight line connecting the points at the ends of the interval is used to interpolate the position of the root. The intersection of this line with the x-axis determines the value of $x_j$ used in the next step. This value $x_j$ is given by

```
$x_j = x_i - f(x_i) \cdot \frac{x_j - x_i}{f(x_j) - f(x_i)}$
```

in place of the midpoint. Convergence is faster than the bisection method. However, the interval will converge closer to the root from one side.

The modified regula falsi method is the same as the regula falsi method, except for the following change: In each iteration, the full interval is replaced by the subinterval containing the root, a relaxation factor is used to modify the function's value at the fixed end of the subinterval. A relaxation factor of approximately 0.9 is suggested. This added feature causes the interval to converge from both ends, and convergence is then based on interval size. This method is the preferred procedure for finding a root of a function that isn't too expensive to evaluate and is known to have a root in a specified interval.
```
function Y = BoxMuller(N)
% Generates N bivariate normally distributed variables avoiding the
% use of the trigonometric functions.
Y = zeros(N,2);
for n = 1:N
    % Generate random number within the unit circle.
    while w >= 1
        x1 = 2.0 * rand - 1.0;
        x2 = 2.0 * rand - 1.0;
        w = x1 * x1 + x2 * x2;
    end
    w = sqrt( (-2.0 * log( w ) ) / w );
    Y(n,1) = x1 * w;
    Y(n,2) = x2 * w;
end
```

Listing 3.2: Polar Box—Muller transform.

# 3.2 Rejection Sampling

We now consider the case where the probability density function f is available and can be evaluated, but the cumulative distribution function F is not, and inverse transform sampling is not an option. Let g be a probability density function such that f(x) <= cg(x) for all x for some finite constant c > 1. Let G be the associated cumulative distribution function. We also assume that we have a method to draw samples from the distribution given by G. That is g(x) is a simpler probability density function and cg(x) is an envelope to f(x). Figure 3.4 shows three choices for cg(x) for a probability density function f which has two modes. The first choice is a uniform distribution over the support of f. That is the range of x where f(x) is non-zero. For the other two, g is normally distributed. For the second choice the mean of g is at the same location as one of the modes of f, while for the third choice the mean lies between the two modes. We see that there are infinitely many possibilities for g.

Rejection sampling, also known as the acceptance-rejection method, proceeds as follows:

+   1. Draw a random variable $x$ following the distribution given by $g$;
+   2. Draw a random variable $u$ from the uniform distribution over $(0, 1)$;
+   3. If
+      $$u \le \frac{f(x)}{cg(x)},$$ (3.3)
+      accept $x$ as a sample from the distribution given by $f$. Otherwise return to 1.
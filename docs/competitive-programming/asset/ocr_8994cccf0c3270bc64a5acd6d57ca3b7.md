Using `extendedEuclid`, the Linear Diophantine Equation with two variables can be easily solved.

For our motivating problem above: $25x + 18y = 839$, we have:

$a = 25, b = 18, \text{extendedEuclid}(25, 18) = ((-5, 7), 1)$, or

$25 \times (-5) + 18 \times 7 = 1$.

Multiplying the left and right hand side of the equation above by $839/\gcd(25, 18) = 839$, we have:

$25 \times (-4195) + 18 \times 5873 = 839$. Thus,

$x = -4195 + (18/1)n,\ y = 5873 - (25/1)n$.

Since we need to have non-negative $x$ and $y$, we have:

$-4195 + 18n \geq 0$ and $5873 - 25n \geq 0$, or

$4195/18 \leq n \leq 5873/25$, or

$233.05 \leq n \leq 234.92$.

The only possible integer for $n$ is 234.

Thus $x = -4195 + 18 \times 234 = 17$ and $y = 5873 - 25 \times 234 = 23$,

i.e. 17 apples (of 25 cents each) and 23 oranges (of 18 cents each) of a total of 8.39 SGD.

+   Programming Exercises related to Extended Euclid algorithm:
+   
+   1. UVa 718 - Skycraper Floors
+   2. UVa 10090 - Marbles (use solution for Linear Diophantine Equation)
+   3. UVa 10104 - Euclid Problem (pure problem involving Extended Euclid)

# 5.3.5  Modulo Arithmetic

Some mathematics computations in programming problems can end up having very large positive (or very small negative) results that reside the range of largest integer data type (currently the 64-bit `long long` in C++). Sometimes, we are only interested with the result modulo a number.

For example in UVa 10176 - Ocean Deep! Make it shallow!!, we are asked to convert a long binary number (up to 100 digits) to decimal. A quick calculation shows that the largest possible number is $2^{100} - 1$ which is beyond the reach of 64-bit integers. However, the problem only ask if the result is divisible by 131071. So what we need to do is to convert binary to decimal digit by digit, and then quickly perform modulo operation to the intermediate result by 131071. If the final result is 0, then the actual number in binary (which we never compute), is divisible by 131071.

+   Programming Exercises related to Modulo Arithmetic:
+   
+   1. UVa 374 - Big Mod
+   2. UVa 602 - What Day Is It?
+   3. UVa 10174 - Couple-Bachelor-Spinster Numbers
+   4. UVa 10176 - Ocean Deep! Make it shallow!! (as discussed above)
+   5. UVa 10212 - The Last Non-zero Digit
+   6. UVa 10489 - Boxes of Chocolates
+   7. LA 4104 - MODEX
\( N = P_1 P_2 P_3 \cdots P_k + 1 \)

Clearly, \( N \) is larger than \( P_k \), so, by assumption, \( N \) is not prime. However, none of \( P_1, P_2, ..., P_k \) divides \( N \) exactly, because there will always be a remainder of 1. This is a contradiction, because every number is either prime or a product of primes. Hence, the original assumption, that \( P_k \) is the largest prime, is false, which implies that the theorem is true.

# 1.3 A Brief Introduction to Recursion

Most mathematical functions that we are familiar with are described by a simple formula. For instance, we can convert temperatures from Fahrenheit to Celsius by applying the formula

\( C = 5(F - 32)/9 \)

Given this formula, it is trivial to write a C++ function, with declarations and braces removed, the one-line formula translates to one line of C++.

Mathematical functions are sometimes defined in a less standard form. As an example, we can define a function \( f \), valid on nonnegative integers, that satisfies \( f(0) = 0 \) and \( f(x) = 2(x - 1) + x^2 \). From this definition we see that \( f(1) = 1 \), \( f(2) = 6 \), \( f(3) = 21 \), and \( f(4) = 58 \). A function that is defined in terms of itself is called **recursive**. C++ allows functions to be recursive. It is important to remember that what C++ provides is merely an attempt to follow the recursive spirit. Not all mathematically recursive functions are efficiently (or correctly) implemented by C++ simulation. The idea is that the recursive function \( f \) ought to be expressible in only a few lines, just like a nonrecursive function. Figure 1.2 shows the recursive implementation of \( f \).

Lines 3 and 4 handle what is known as the **base case**, that is, the value for which the function is directly known without resorting to recursion. Just as declaring \( f(x) = 2(x - 1) + x^2 \) is meaningless, mathematically, without including the fact that \( f(0) = 0 \), the recursive C++ function doesn't make sense without a base case. Line 6 makes the recursive call.

```
1 int f( int x )
2 {
3
4    if( x == 0 )
5       return 0;
6    else
7       return 2 * f( x - 1 ) + x * x;
8 }
```

**Figure 1.2** A recursive function
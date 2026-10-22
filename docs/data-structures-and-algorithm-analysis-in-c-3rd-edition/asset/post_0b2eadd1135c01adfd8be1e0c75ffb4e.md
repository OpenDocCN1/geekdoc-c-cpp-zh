
The first two properties state that the logarithm of two numbers multiplied (or divided) can be found by adding (or subtracting) the logarithms of the two numbers.⁴ Property (3) is simply an extension of property (1). Property (4) tells us that, for variable n and any two integer constants a and b, logₐ n and logᵦ n differ by the constant factor logᵦ a, regardless of the value of n. Most runtime analyses in this book are of a type that ignores constant factors in costs. Property (4) says that such analyses need not be concerned with the base of the logarithm, because this can change the total cost only by a constant factor. Note that 2^{log n} = n.

When discussing logarithms, exponents often lead to confusion. Property (3) tells us that log n² = 2 log n. How do we indicate the square of the logarithm (as opposed to the logarithm of n²)? This could be written as (log n)², but it is traditional to use log² n. On the other hand, we might want to take the logarithm of the logarithm of n. This is written log log n.

A special notation is used in the rare case when we need to know how many times we must take the log of a number before we reach a value ≤ 1. This quantity is written log* n. For example, log* 1024 = 4 because log 1024 = 10, log 10 ≈ 3.33, log 3.33 ≈ 1.74, and log 1.74 < 1, which is a total of 4 log operations.

## 2.4 Summations and Recurrences

Most programs contain loop constructs. When analyzing running time costs for programs with loops, we need to add up the costs for each time the loop is executed. This is an example of a summation. Summations are simply the sum of costs for some function applied to a range of parameter values. Summations are typically written with the following “Sigma” notation:

∑_{i=1}^{n} f(i).

This notation indicates that we are summing the value of f(i) over some range of (integer) values. The parameter to the expression and its initial value are indicated below the ∑ symbol. Here, the notation i = 1 indicates that the parameter is i and that it begins with the value 1. At the top of the ∑ symbol is the expression n. This indicates the maximum value for the parameter i. Thus, this notation means to sum the values of f(i) as i ranges across the integers from 1 through n. This can also be written f(1) + f(2) + ⋯ + f(n − 1) + f(n). Within a sentence, Sigma notation is typeset as ∑_{i=1}^{n} f(i).

Given a summation, you often wish to replace it with an algebraic equation with the same value as the summation. This is known as a closed-form solution, and the process of replacing the summation with its closed-form solution is known as solving the summation. For example, the summation ∑_{i=1}^{n} 1 is simply the expression “1” summed n times (remember that i ranges from 1 to n). Because the sum of n 1s is n, the closed-form solution is n. The following is a list of useful summations, along with their closed-form solutions.

∑_{i=1}^{n} i = n(n + 1)/2. (2.1)

∑_{i=1}^{n} i² = (2n³ + 3n² + n)/6 = n(2n + 1)(n + 1)/6. (2.2)

∑_{i=1}^{n} n = n log n. (2.3)

∑_{i=0}^{∞} a^i = 1/(1 − a) for 0 < a < 1. (2.4)

∑_{i=0}^{n} a^i = (a^{n+1} − 1)/(a − 1) for a ≠ 1. (2.5)

As special cases to Equation 2.5,

∑_{i=1}^{n} 1/2^i = 1 − 1/2^n. (2.6)

and

∑_{i=0}^{n} 2^i = 2^{n+1} − 1. (2.7)

As a corollary to Equation 2.7,

∑_{i=0}^{log n} 2^i = 2^{log n +1} − 1 = 2n − 1. (2.8)

Finally,

∑_{i=1}^{n} i/2^i = 2 − (n + 2)/2^n. (2.9)

The sum of reciprocals from 1 to n, called the Harmonic Series and written ℋ_n, has a value between log_e n and log_e n + 1. To be more precise, as n grows, the summation grows closer to

H_n ≈ log_e n + γ + 1/(2n), (2.10)

where γ is Euler’s constant and has the value 0.5772...

Most of these equalities can be proved easily by mathematical induction (see Section 2.6.3). Unfortunately, induction does not help us derive a closed-form solution. It only confirms when a proposed closed-form solution is correct. Techniques for deriving closed-form solutions are discussed in Section 14.1.

The running time for a recursive algorithm is most easily expressed by a recursive expression because the total time for the recursive algorithm includes the time to run the recursive call(s). A recurrence relation defines a function by means of an expression that includes one or more (smaller) instances of itself. A classic example is the recursive definition for the factorial function:

```
n! = (n-1)! · n for n > 1; 1! = 0! = 1.
```

```
Fib(n) = Fib(n-1) + Fib(n-2) for n > 2; Fib(1) = Fib(2) = 1.
```

From this definition, the first seven numbers of the Fibonacci sequence are

- 1, 1, 2, 3, 5, 8, and 13.

Notice that this definition contains two parts: the general definition for Fib(n) and the base cases for Fib(1) and Fib(2). Likewise, the definition for factorial contains a recursive part and base cases.

Recurrence relations are often used to model the cost of recursive functions. For example, the number of multiplications required by function fact of Section 2.5 for an input of size n will be zero when n = 0 or n = 1 (the base cases), and it will be one plus the cost of calling fact on a value of n-1. This can be defined using the following recurrence:

```
T(n) = T(n-1) + 1 for n > 1; T(0) = T(1) = 0.
```

As with summations, we typically wish to replace the recurrence relation with a closed-form solution. One approach is to expand the recurrence by replacing any occurrences of T on the right-hand side with its definition.

### Example 2.8 If we expand the recurrence T(n) = T(n-1) + 1, we get

```
T(n) = T(n-1) + 1
= (T(n-2) + 1) + 1
```

We can expand the recurrence as many steps as we like, but the goal is to detect some pattern that will permit us to rewrite the recurrence in terms of a summation. In this example, we might notice that

```
(T(n − 2) + 1) + 1 = T(n − 2) + 2
```

and if we expand the recurrence again, we get

```
T(n) = T(n − 2) + 2 = T(n − 3) + 1 + 2 = T(n − 3) + 3
```

which generalizes to the pattern T(n) = T(n − i) + i. We might conclude that

```
T(n) = T(n − (n − 1)) + (n − 1)
= T(1) + n − 1
= n − 1.
```

Because we have merely guessed at a pattern and not actually proved that this is the correct closed form solution, we should use an induction proof to complete the process (see Example 2.13).

### Example 2.9 A slightly more complicated recurrence is

```
T(n) = T(n − 1) + n;   T(1) = 1.
```

Expanding this recurrence a few steps, we get

```
T(n) = T(n − 1) + n
= T(n − 2) + (n − 1) + n
= T(n − 3) + (n − 2) + (n − 1) + n.
```

We should then observe that this recurrence appears to have a pattern that leads to

```
T(n) = T(n − (n − 1)) + (n − (n − 2)) + ⋯ + (n − 1) + n
= 1 + 2 + ⋯ + (n − 1) + n.
```

This is equivalent to the summation ∑_{i=1}^{n} i, for which we already know the closed-form solution.

Techniques to find closed-form solutions for recurrence relations are discussed in Section 14.2. Prior to Chapter 14, recurrence relations are used infrequently in this book, and the corresponding closed-form solution and an explanation for how it was derived will be supplied at the time of use.

## 2.5 Recursion

An algorithm is recursive if it calls itself to do part of its work. For this approach to be successful, the “call to itself” must be on a smaller problem then the one originally attempted. In general, a recursive algorithm must have two parts: the base case, which handles a simple input that can be solved without resorting to a recursive call, and the recursive part which contains one or more recursive calls to the algorithm where the parameters are in some sense “closer” to the base case than those of the original call. Here is a recursive C++ function to compute the factorial of n. A trace of fact’s execution for a small value of n is presented in Section 4.2.4.

```
long fact(int n) {          // Compute n! recursively
    // To fit n! into a long variable, we require n <= 12
    Assert((n >= 0) && (n <= 12), "Input out of range");
    if (n <= 1) return 1; // Base case: return base solution
    return n * fact(n-1);   // Recursive call for n > 1
}
```

The first two lines of the function constitute the base cases. If n ≤ 1, then one of the base cases computes a solution for the problem. If n > 1, then fact calls a function that knows how to find the factorial of n − 1. Of course, the function that knows how to compute the factorial of n − 1 happens to be fact itself. But we should not think too hard about this while writing the algorithm. The design for recursive algorithms can always be approached in this way. First write the base cases. Then think about solving the problem by combining the results of one or more smaller — but similar — subproblems. If the algorithm you write is correct, then certainly you can rely on it (recursively) to solve the smaller subproblems. The secret to success is: Do not worry about how the recursive call solves the subproblem. Simply accept that it will solve it correctly, and use this result to in turn correctly solve the original problem. What could be simpler?

Recursion has no counterpart in everyday, physical-world problem solving. The concept can be difficult to grasp because it requires you to think about problems in a new way. To use recursion effectively, it is necessary to train yourself to stop analyzing the recursive process beyond the recursive call. The subproblems will take care of themselves. You just worry about the base cases and how to recombine the subproblems.

The recursive version of the factorial function might seem unnecessarily complicated to you because the same effect can be achieved by using a while loop. Here is another example of recursion, based on a famous puzzle called “Towers of Hanoi.” The natural algorithm to solve this problem has multiple recursive calls. It cannot be rewritten easily using while loops.

The Towers of Hanoi puzzle begins with three poles and n rings, where all rings start on the leftmost pole (labeled Pole 1). The rings each have a different size, and

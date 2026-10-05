# 34

Chap. 2 Mathematical Preliminaries

summation grows closer to

```
$$\mathcal{H}_n \approx \log_n n + \gamma + \frac{1}{2n} \quad (2.10)$
```

where $\gamma$ is Euler's constant and has the value 0.5772...

Most of these equalities can be proved easily by mathematical induction (see Section 2.6.3). Unfortunately, induction does not help derive a closed-form solution. It only confirms if a proposed closed-form solution is correct. Techniques for deriving closed-form solutions are discussed in Section 14.1.

The running time for a recursive algorithm is most easily expressed by a recursive expression because the total time for the recursive algorithm includes the time to run the recursive call(s). A **recurrence relation** defines a function by means of an expression that includes one or more (smaller) instances of itself. A classic example is the recursive factorial:

```
$n! = (n-1)! \cdot n > 1; \quad ! = 0! = 1.$
```

Another example of a recurrence is the Fibonacci sequence:

```
$Fib(n) = Fib(n-1) + Fib(n-2) \text{ for } n > 2; \quad Fib(1) = Fib(2) = 1.$
```

From this definition, the first seven numbers of the Fibonacci sequence

```
$1, 1, 2, 3, 5, 8, and 13.$
```

Notice that this definition contains two parts: the general definition for $Fib(n)$ and the base cases for $Fib(1)$ and $Fib(2)$. Likewise, the definition for factorial contains a recursive part and base cases.

Recurrence relations are often used to model the cost of recursive functions. For example, the number of multiplications required by function **fact** of Section 2.5 for an input of size $n$ will be zero when $n=0$ or $n=1$ (the base cases), and it will be one plus the cost of calling **fact** on a value of $n-1$. This can be defined using the following recurrence:

```
$T(n) = T(n-1) + 1 \text{ for } n > 1; \quad T(0) = T(1) = 0.$
```

With summations, we typically wish to replace the recurrence relation with a closed-form solution. One approach is to **expand** the recurrence by replacing any occurrences of $T$ on the right-hand side with its definition.

**Example 2.8** If we expand the recurrence $T(n) = T(n-1) + 1$, we get

```
$T(n) = T(n-1) + 1\n= T(n-2) + 1.$
```

## 14.1 Summation Techniques

Consider the following simple summation.

$$\sum_{i=1}^{n} i.$$

In Section 2.6.3 it was proved by induction that this summation has the well-known closed form n(n + 1)/2. But while induction is a good technique for proving that a proposed closed-form expression is correct, how do we find a candidate closed-form expression to test in the first place? Let us try to think through this problem from first principles, as though we had never seen it before.

A good place to begin analyzing a summation is to give an estimate of its value for a given n. Observe that the biggest term for this summation is n, and there are n terms being summed up. So the total must be less than n². Actually, most terms are much less than n, and the sizes of the terms grow linearly. If we were to draw a picture with bars for the size of the terms, their heights would form a line, and we could enclose them in a box n units wide and n units high. It is easy to see from this that a closer estimate for the summation is about (n²)/2. Having this estimate in hand helps us when trying to determine an exact closed-form solution, because we will hopefully recognize if our proposed solution is badly wrong.

Let us now consider some ways that we might hit upon an exact equation for the closed form solution to this summation. One particularly clever approach we can take is to observe that we can “pair up” the first and last terms, the second and (n − 1)th terms, and so on. Each pair sums to n + 1. The number of pairs is n/2. Thus, the solution is n(n + 1)/2. This is pretty, and there is no doubt about it being correct. The problem is that it is not a useful technique for solving many other summations.

Now let us try to do something a bit more general. We already recognized that, because the largest term is n and there are n terms, the summation is less than n². If we are lucky, the closed form solution is a polynomial. Using that as a working assumption, we can invoke a technique called guess-and-test. We will guess that the closed-form solution for this summation is a polynomial of the form c₁n² + c₂n + c₃ for some constants c₁, c₂, and c₃. If this is true, then we can plug in the answers to small cases of the summation to solve for the coefficients. For this example, substituting 0, 1, and 2 for n leads to three simultaneous equations. Because the summation when n = 0 is just 0, c₃ must be 0. For n = 1 and n = 2 we get the two equations

$$c₁ + c₂ = 1$$

$$4c₁ + 2c₂ = 3.$$

Dividing f(n) by both n and f(n − 1) happens to give us useful patterns to work with. f(n)/n = (n + 1)/2, and f(n)/f(n − 1) = (n + 1)/(n − 1). Of course, lots of other guesses for function g do not work. For example, f(n) − n = f(n − 1). Knowing that f(n) = f(n − 1) + n is not useful for determining the closed form solution to this summation. Or consider f(n) − f(n − 1) = n. Again, knowing that f(n) = f(n − 1) + n is not useful. Finding the right combination of equations can be like finding a needle in a haystack.

In our first example, we can see directly what the closed-form solution should be. Since f(n)/n = (n + 1)/2, obviously f(n) = n(n + 1)/2.

Dividing f(n) by f(n − 1) does not give so obvious a result, but it provides another useful illustration.

```
f(n)/f(n − 1) = (n + 1)/(n − 1)
f(n)(n − 1) = (n + 1)f(n − 1)
f(n)(n − 1) = (n + 1)(f(n) − n)
nf(n) − f(n) = nf(n) + f(n) − n² − n
2f(n) = n² + n = n(n + 1)
f(n) = n(n + 1)/2
```

Once again, we still do not have a proof that f(n) = n(n + 1)/2. Why? Because we did not prove that f(n)/n = (n + 1)/2 nor that f(n)/f(n − 1) = (n + 1)/(n − 1). We merely hypothesized patterns from looking at a few terms. Fortunately, it is easy to check our hypothesis with induction.

### Example 14.2

Solve the summation

$$\sum_{i=1}^{n} \frac{1}{2^{i}}.$$

We will begin by writing out a table listing the first few values of the summation, to see if we can detect a pattern.

| n | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|
| f(n) | 1/2 | 3/4 | 7/8 | 15/16 | 31/32 | 63/64 |
| 1 − f(n) | 1/2 | 1/4 | 1/8 | 1/16 | 1/32 | 1/64 |

By direct inspection of the second line of the table, we might recognize the pattern f(n) = (2^{n} − 1)/2^{n}. A simple induction proof can then prove that this always holds true. Alternatively, consider if we hadn’t noticed the pattern for the form of f(n). We might observe that f(n) appears to be reaching an asymptote at one. In which case, we might consider looking at the difference between f(n) and the expected asymptote. This result is shown in the last line of the table, which has a clear pattern since the i-th entry is 1/2^{i}. From this we can easily deduce a guess that f(n) = 1 − 1/2^{n}. Again, a simple induction proof will verify the guess.

### Example 14.3

Solve the summation

$$f(n) = \sum_{i=0}^{n} a r^{i} = a + ar + ar^{2} + \cdots + ar^{n}.$$

This is called a geometric series. Our goal is to find some function g(n) such that the difference between f(n) and g(n) leaves us with an easily manipulated equation. Because consecutive terms of the summation differ by a factor of r, we can shift terms if we multiply the entire expression by r:

$$r f(n) = r \sum_{i=0}^{n} a r^{i} = ar + ar^{2} + ar^{3} + \cdots + ar^{n+1}.$$

We can now subtract the one equation from the other, as follows:

$$f(n) - r f(n) = a + ar + ar^{2} + ar^{3} + \cdots + ar^{n} - (ar + ar^{2} + ar^{3} + \cdots + ar^{n}) - ar^{n+1}.$$

The result leaves only the end terms:

$$f(n) - r f(n) = \sum_{i=0}^{n} a r^{i} - r \sum_{i=0}^{n} a r^{i}$$

$$(1 - r) f(n) = a - a r^{n+1}.$$

Thus, we get the result

$$f(n) = \frac{a - a r^{n+1}}{1 - r}$$

where r ≠ 1.

### Example 14.4

For our second example of the shifting method, we solve

$$f(n) = \sum_{i=1}^{n} i 2^{i} = 1 \cdot 2^{1} + 2 \cdot 2^{2} + 3 \cdot 2^{3} + \cdots + n \cdot 2^{n}.$$

We can achieve our goal if we multiply by two:

$$2f(n) = 2 \sum_{i=1}^{n} i 2^{i} = 1 \cdot 2^{2} + 2 \cdot 2^{3} + 3 \cdot 2^{4} + \cdots + (n - 1) \cdot 2^{n} + n \cdot 2^{n+1}.$$

The i-th term of 2f(n) is i · 2^{i+1}, while the (i + 1)-th term of f(n) is (i + 1) · 2^{i+1}. Subtracting one expression from the other yields the sum of 2^{i} and a few non-canceled terms:

$$2f(n) - f(n) = 2 \sum_{i=1}^{n} i 2^{i} - \sum_{i=1}^{n} i 2^{i} = \sum_{i=1}^{n} i 2^{i+1} - \sum_{i=1}^{n} i 2^{i}.$$

Shift i's value in the second summation, substituting (i + 1) for i:

$$= n 2^{n+1} + \sum_{i=0}^{n-1} i 2^{i+1} - \sum_{i=0}^{n-1} (i + 1) 2^{i+1}.$$

Break the second summation into two parts:

$$= n 2^{n+1} + \sum_{i=0}^{n-1} i 2^{i+1} - \sum_{i=0}^{n-1} i 2^{i+1} - \sum_{i=0}^{n-1} 2^{i+1}.$$

Cancel like terms:

$$= n 2^{n+1} - \sum_{i=0}^{n-1} 2^{i+1}.$$

Again shift i's value in the summation, substituting i for (i + 1):

$$= n 2^{n+1} - \sum_{i=1}^{n} 2^{i}.$$

Replace the new summation with a solution that we already know:

$$= n 2^{n+1} - (2^{n+1} - 2).$$

Finally, reorganize the equation:

$$= (n - 1) 2^{n+1} + 2.$$

## 14.2 Recurrence Relations

Recurrence relations are often used to model the cost of recursive functions. For example, the standard Mergesort (Section 7.4) takes a list of size n, splits it in half, performs Mergesort on each half, and finally merges the two sublists in n steps. The cost for this can be modeled as

$$T(n) = 2T(n/2) + n$$

In other words, the cost of the algorithm on input of size n is two times the cost for input of size n/2 (due to the two recursive calls to Mergesort) plus n (the time to merge the sublists together again).

There are many approaches to solving recurrence relations, and we briefly consider three here. The first is an estimation technique: Guess the upper and lower bounds for the recurrence, use induction to prove the bounds, and tighten as required. The second approach is to expand the recurrence, convert it to a summation, and then use summation techniques. The third approach is to take advantage of already proven theorems when the recurrence is of a suitable form. In particular, typical divide and conquer algorithms such as Mergesort yield recurrences of a form that fits a pattern for which we have a ready solution.

### 14.2.1 Estimating Upper and Lower Bounds

The first approach to solving recurrences is to guess the answer and then attempt to prove it correct. If a correct upper or lower bound estimate is given, an easy induction proof will verify this fact. If the proof is successful, then try to tighten the bound. If the induction proof fails, then loosen the bound and try again. Once the upper and lower bounds match, you are finished. This is a useful technique when you are only looking for asymptotic complexities. When seeking a precise closed-form solution (i.e., you seek the constants for the expression), this method will probably be too much work.

### Example 14.5

Use the guessing technique to find the asymptotic bounds for Mergesort, whose running time is described by the equation

$$T(n) = 2T(n/2) + n; \quad T(2) = 1$$

We begin by guessing that this recurrence has an upper bound in O(n²). To be more precise, assume that

$$T(n) \le n^{2}$$

We prove this guess is correct by induction. In this proof, we assume that n is a power of two, to make the calculations easy. For the base case,

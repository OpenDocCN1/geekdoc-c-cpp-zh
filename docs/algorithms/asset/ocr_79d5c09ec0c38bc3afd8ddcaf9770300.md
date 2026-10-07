# Chapter 0

# Algorithms 3

No other sequence of numbers has been studied extensively, or applied to more fields: biology, demography, art, architecture, music, to name just a few. And, together with the powers of 2, it is computer science's favorite sequence.

In fact, the Fibonacci numbers grow almost as the powers of 2: for example, $F_{30}$ is over a million, and $F_{100}$ is already 21 digits long! In general, $F_n \approx 2^{0.694n}$ (see Exercise 0.3).

But what is the precise value of $F_{100}$, or $F_{200}$? Fibonacci himself would wanted to know such things. To answer, we need an algorithm for computing the $n$th Fibonacci number.

![](bbox=[0.343, 0.277, 0.891, 0.506])

# An exponential algorithm

One idea is to slavishly implement the recursive definition of $F_n$. Here is the resulting algorithm, in the “pseudocode” notation used throughout this book:

```
function fib1(n)
  if n = 0: return 0
  if n = 1: return 1
  return fib1(n-1) + fib1(n-2)
```

Whenever we have an algorithm, correct? there are three questions we always ask about it:

+   1. Is it correct?
2. How much time does it take, as a function of $n$?
3. And can we do better?

The first question is most here, as this algorithm is precisely Fibonacci’s definition of $F_n$. The second demands an answer. Let $T(n)$ be the number of computer steps needed to compute `fib1(n)`; what can we say about this function? For starters, if $n$ is less than 2, the procedure halts almost immediately, after just a couple of steps. Therefore,

$T(n) \le 2$ for $n \le 1$.
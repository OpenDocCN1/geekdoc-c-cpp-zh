# Chapter 1

# Fundamentals

# 1.1 Approximating the square root of a number

# Problem Description

Write a program that, given a fixed integer n ≥ 0, establishes the truth of

$$R : 0 ≤ a² ≤ n < (a + 1)²$$

# Solution

Taking the square root of all terms in R, we find that R is equivalent to 0 ≤ a ≤ √n < a + 1. Hence, a is the largest integer that is at most √n. The first step is to rewrite R as a set of conjuncts:

$$R : 0 ≤ a² ∧ a² ≤ n ∧ n < (a + 1)²$$

Deleting the third conjunct of R yields a possible invariant:

$$P : 0 ≤ a² ≤ n.$$

Because n ≥ 0, P can be established by the assignment a ← 0. For the condition of the loop, use the complement of the deleted conjunct, so that when the loop terminates because the condition is false, the deleted conjunct is true. This yields the almost completed program :

```
```
1: a ← 0
2: while (a + 1)² ≤ n do
3:   ?
4: end while
```
```

The purpose of the command of the loop is to progress towards termination. Clearly, if the condition of the loop is true then a is too
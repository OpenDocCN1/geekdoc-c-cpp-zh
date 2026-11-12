# 7.3 The Parallel Prefix Problem

Let $\bullet$ be an arbitrary associative binary operation $\bullet$; namely it satisfies
$$x \bullet (y \bullet z) = (x \bullet y) \bullet z.$$
which we will simply call product. For example, $\bullet$ can represent addition, multiplication, or maximum of two numbers.

# Problem Description

Given a sequence of numbers $x_1, x_2, \ldots, x_n$, compute the products $x_1 \bullet x_2 \bullet \cdots \bullet x_k$, for all $k$, such that $1 \leq k \leq n$.

# Solution

We denote by $PR(i,j)$ the product $x_i \bullet x_{i+1} \bullet \cdots \bullet x_j$. Our goal is to compute $PR(1,k)\,\forall k,\,1 \leq k \leq n$. The sequential version of the prefix problem is trivial; we simply compute the prefixes in order. The parallel prefix problem is not as easy to solve. The method we use is divide and conquer. As usual, we assume that $n$ is a power of 2.

# Induction Hypothesis

*We know how to solve the parallel prefix problem for $\frac{n}{2}$ elements.*

The case of one element is trivial. The algorithm proceeds by dividing the input in half, and solving each half by induction. Thus, we obtain the values of $PR(1,k)$ and $PR(\frac{n}{2}+1,\frac{n}{2}+k)\,\forall k,\,1 \leq k \leq \frac{n}{2}$. The values for the first half can be used directly. The values $PR(1,m)$, for $\frac{n}{2} < m \leq n$ can be obtained by computing $PR(1,\frac{n}{2}) \bullet PR(\frac{n}{2}+1,m)$. Both terms are known by induction. Please note that we use the associativity of the operation. The complete algorithm is given below.
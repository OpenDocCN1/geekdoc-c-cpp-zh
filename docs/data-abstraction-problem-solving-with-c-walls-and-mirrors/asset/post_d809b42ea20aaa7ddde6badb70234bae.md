
# 294 CHAPTER 10 Algorithm Efficiency

# FIGURE 10-1 Time requirements as a function of the problem size $n$

![](img/d0cb86b2f18b2db569968ad7c743510e_320_0.png)

conclusion such as '$A$ time proportional to $n^2$' is exactly the kind of statement that characterizes the inherent efficiency of an algorithm independently of such factors as particular computers and implementations.

Figure 10-1 also shows that $A$'s time requirement does not exceed $B$'s until $n$ exceeds 25. Algorithm efficiency is typically a concern for large problems only. The requirements for small problems are generally not large enough to matter. Thus, our analysis assume large values of $n$.

> Note: When comparing the efficiency of various solutions, look only at significant differences. This rule is consistent with a multidimensional view of the cost of a computer program.

## 10.2.3 Analysis and Big O Notation

If $Algorithm A$ requires time proportional to $f(n)$, $Algorithm$ is said to be of order $f(n)$, which is denoted as $O(f(n))$. The function $f(n)$ is called the algorithm's growth-rate function. The notation uses the capital letter $O$ to denote order, it is called the Big O Notation. If a problem of size $n$ requires time that is directly proportional to $n$, the problem is $O(n)$—that is, order $n$. If the time requirement is directly proportional to $n^2$, the problem is $O(n^2)$, and so on.

The following formalization defines this:

> Note: Definition of the order of an algorithm
Algorithm A is of order $f(n)$—denoted $O(f(n))$—if constants $k$ and $n_0$ exist such that $A$ requires no more than $k \times f(n)$ time units to solve a problem of size $n \ge n_0$

The requirement $n \ge n_0$ in the definition of $O(f(n))$ formalizes the notion of sufficiently large problems. In general, many values of $k$ and $n$ can satisfy the definition.

## Measuring the Efficiency of Algorithms

The following examples illustrate the definition:

- Suppose that an algorithm requires $n^2 - 3 \times n + 10$ to solve a problem of size $n$. If constants $k$ and $n_0$ exist such that $k \times n^2 > n^2 - 3 \times n + 10$ for all $n \ge n_0$, the algorithm is $O(n^2)$. In fact, if $k$ is 3 and $n_0$ is 2, $3 \times n^2 > n^2 - 3 \times n + 10$ for all $n \ge 2$ as Figure 10-2 illustrates. Thus, the algorithm requires no more than $k \times n^2$ time units for $n \ge n_0$, and so is $O(n^2)$.

- Previously in Section 10.2.1, we found that displaying a linked chain's first $n$ items requires $(n+1)(a+c) + n \times w$ time units. Because $2 \times n \ge n+1$ for $n \ge 1$, $(2 \times n) \times (a+c) + n \times w \ge (n+1) \times (a+c) + n \times w$ for $n \ge 1$. After factoring $n$ on the left side of the equation, we have $(2 \times a + 2 \times c + w) \times n \ge (n+1) \times (a+c) + n \times w$ for $n \ge 1$.

- Thus, the task is $O(n)$. Here, $k$ is $2 \times a + 2 \times c$ with $w$ and $n_0$ is 1.

Similarly, the solution to the definition of Towers of Hanoi problem requires $(2^m-1) \times m$ time units. Because $m \times 2^m > (2^m-1) \times m$ for $n \ge 1$, the solution is $O(n^2)$.

The requirement $n \ge n_0$ in the definition of $O(f(n))$ means that the time estimate is correct for sufficiently large problems. In other words, the time estimate is too small for most a finite number of problem sizes. For example, the function $\log n$ takes the value 0 when $n$ is 1. The fact that $k \log 1$ is 0 for all constants implies an unrealistic time requirement; presumably, all algorithms require more than 0 time units, even to solve a problem of size 1. Thus, you can discount problems of size = 1 if $f(n)$ is $\log n$.

FIGURE 10-2 The graphs of $3 \times n^2$ and $n^2 - 3 \times n + 10$

![](img/d0cb86b2f18b2db569968ad7c743510e_321_0.png)

# 296 CHAPTER 10 Algorithm Efficiency

To dramatize further the significance of an algorithm's proportional growth rate, consider the table and graph in Figure 10-3. The table in part *a*, for various values of *n*, the approximate values of some growth-rate functions, which are listed in order of:

Order of growth of some common functions
$O(1) < O(\log n) < O(n) < O(n \times \log n) < O(n^2) < O(2^n)$

The table demonstrates the relative speed with which the values of the functions grow. Figure 10-3 shows these growth-rate functions have the following intuitive interpretations:

Intuitive interpretations of growth-rate functions

- A growth-rate function of 1 implies a problem whose time requirement is constant and, independent of the problem's size $n$.

- The time requirement for a logarithmic algorithm increases slowly as the problem size increases. If you square the problem size, you only double its time requirement. You will see that you studied in Chapter 2 has this behavior. Recall that a binary search halves an array and searches for one of the halves.

- The base of $\log n$ does not affect the growth rate, you can omit it.

- The time requirement for $O(n)$, **linear**, increases directly with the size.

- The time requirement for $O(n \times \log n)$, increases more than linear.

- The time requirement for $O(n^2)$, **quadratic**, increases directly with the size.

- The time requirement for $O(2^n)$, **exponential**, increases more rapidly.

If a problem of size $n$ requires time that is directly proportional to $n$, the problem is $O(n)$—that is, order $n$. If the time requirement is directly proportional to $n^2$, the problem is $O(n^2)$, and so on.

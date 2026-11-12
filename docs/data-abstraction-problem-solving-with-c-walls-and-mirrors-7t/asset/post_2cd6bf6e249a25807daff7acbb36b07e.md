
conclusion such as “A requires time proportional to n^2” is exactly the kind of statement that characterizes the inherent efficiency of an algorithm independently of such factors as particular computers and implementations.

FIGURE 10-1 Time requirements as a function of the problem size n

![](img/288a0c22d14d2450c1e772f228f867b0_320_0.png)

Figure 10-1 also shows that A’s time requirement does not exceed B’s until n exceeds 25. Algorithm efficiency is typically a concern for large problems only. The time requirements for small problems are generally not large enough to matter. Thus, our analyses assume large values of n.

> Note: When comparing the efficiency of various solutions, look only at significant differences. This rule is consistent with a multidimensional view of the cost of a computer program.

## 10.2.3 Analysis and Big O Notation

*If Algorithm A requires time proportional to f(n)*

Algorithm A is said to be order f(n), which is denoted as O(f(n)). The function f(n) is called the algorithm’s growth-rate function. Because the notation uses the capital letter O to denote order, it is called the Big O notation. If a problem of size n requires time that is directly proportional to n, the problem is O(n)—that is, order n. If the time requirement is directly proportional to n^2, the problem is O(n^2), and so on.

The following definition formalizes these ideas:

> Note: Definition of the order of an algorithm Algorithm A is order f(n)—denoted O(f(n))—if constants k and n0 exist such that A requires no more than k x f(n) time units to solve a problem of size n >= n0.

The requirement n >= n0 in the definition of O(f(n)) formalizes the notion of sufficiently large problems. In general, many values of k and n0 can satisfy the definition.

The following examples illustrate the definition:

- Suppose that an algorithm requires \(n^2 - 3 \times n + 10\) seconds to solve a problem of size \(n\). If constants \(k\) and \(n_0\) exist such that  
  \(k \times n^2 > n^2 - 3 \times n + 10 \text{ for all } n \ge n_0\)  
  the algorithm is \(O(n^2)\). In fact, if \(k\) is 3 and \(n_0\) is 2,  
  \(3 \times n^2 > n^2 - 3 \times n + 10 \text{ for all } n \ge 2\)  
  as Figure 10-2 illustrates. Thus, the algorithm requires no more than \(k \times n^2\) time units for \(n \ge n_0\), and so is \(O(n^2)\).

- Previously in Section 10.2.1, we found that displaying a linked chain's first \(n\) items requires  
  \((n + 1)(a + c) + n \times w\)  
  time units. Because \(2 \times n \ge n + 1\) for \(n \ge 1\),  
  \((2 \times n) \times (a + c) + n \times w \ge (n + 1) \times (a + c) + n \times w \text{ for } n \ge 1\)  
  After factoring \(n\) on the left side of the inequality, we have  
  \((2 \times a + 2 \times c + w) \times n \ge (n + 1) \times (a + c) + n \times w \text{ for } n \ge 1\)  
  Thus, this task is \(O(n)\). Here, \(k\) is \(2 \times a + 2 \times c + w\) and \(n_0\) is 1.

- Similarly, the solution to the Towers of Hanoi problem requires \((2^n - 1) \times m\) time units. Because  
  \(m \times 2^n > (2^n - 1) \times m \text{ for } n \ge 1\)  
  the solution is \(O(2^n)\).

The requirement \(n \ge n_0\) in the definition of \(O(f(n))\) means that the time estimate is correct for sufficiently large problems. In other words, the time estimate is too small for at most a finite number of problem sizes. For example, the function \(\log n\) takes on the value 0 when \(n\) is 1. Thus, the fact that \(k \times \log n\) is 0 for all constants \(k\) implies an unrealistic time requirement; presumably, all algorithms require more than 0 time units, even to solve a problem of size 1. Thus, you can discount problems of size \(n = 1\) if \(f(n)\) is \(\log n\).

FIGURE 10-2 The graphs of \(3 \times n^2\) and \(n^2 - 3 \times n + 10\)

![](img/288a0c22d14d2450c1e772f228f867b0_321_0.png)

## Order of growth of some common functions

To dramatize further the significance of an algorithm’s proportional growth rate, consider the table and graph in Figure 10-3. The table in part a gives, for various values of n, the approximate values of some common growth-rate functions, which are listed in order of growth:

$O(1) < O(\log_2 n) < O(n) < O(n \times \log_2 n) < O(n^2) < O(n^3) < O(2^n)$

The table demonstrates the relative speed at which the values of the functions grow. Figure 10-3b represents the growth-rate functions graphically.

## Intuitive interpretations of growth-rate functions

These growth-rate functions have the following intuitive interpretations:

- 1  
  A growth-rate function of 1 implies a problem whose time requirement is constant and, therefore, independent of the problem’s size n.

- log2 n  
  The time requirement for a logarithmic algorithm increases slowly as the problem size increases. If you square the problem size, you only double its time requirement. Later you will see that the recursive binary search algorithm that you studied in Chapter 2 has this behavior. Recall that a binary search halves an array and then searches one of the halves. Typical logarithmic algorithms solve a problem by solving a smaller constant fraction of the problem.  
  
  The base of the log does not affect a logarithmic growth rate, so you can omit it in a growth-rate function. Exercise 8 at the end of this chapter asks you to show why this is true.

- n  
  The time requirement for an O(n), or linear, algorithm increases directly with the size of the problem. If you square the problem size, you also square its time requirement.

- n x log2 n  
  The time requirement for an O(n x log2 n) algorithm increases more rapidly than a linear algorithm. Such algorithms usually divide a problem into smaller problems that are each solved separately. The next chapter examines an example of this algorithm type—the merge sort.

- n^2  
  The time requirement for an O(n^2), or quadratic, algorithm increases rapidly with the size of the problem. Algorithms that use two nested loops are often quadratic. Such algorithms are practical only for small problems. The next chapter covers several quadratic sorting algorithms.

- n^3  
  The time requirement for an O(n^3), or cubic, algorithm increases more rapidly with the size of the problem than the time requirement for a quadratic algorithm. Algorithms that use three nested loops are often cubic, and are practical only for small problems.

- 2^n  
  As the size of a problem increases, the time requirement for an exponential algorithm usually increases too rapidly to be practical.

If algorithm A requires time that is proportional to function f and algorithm B requires time that is proportional to a slower-growing function g, it is apparent that B is always significantly more efficient than A for large enough problems. For large problems, the proportional growth rate dominates all other factors in determining an algorithm’s efficiency.

## Properties of growth-rate functions.

Several mathematical properties of Big O notation help to simplify the analysis of an algorithm. As we discuss these properties, you should keep in mind that O(f(n)) means “is of order f(n)” or “has order f(n).” O is not a function.

FIGURE 10-3 A comparison of growth-rate functions: (a) in tabular form; (b) in graphical form

| Function | 10 | 100 | 1,000 | 10,000 | 100,000 | 1,000,000 |
|---|---|---|---|---|---|---|
| 1 | 1 | 1 | 1 | 1 | 1 | 1 |
| log2 n | 3 | 6 | 9 | 13 | 16 | 19 |
| n | 10 | 10^2 | 10^3 | 10^4 | 10^5 | 10^6 |
| n x log2 n | 30 | 664 | 9,965 | 10^5 | 10^6 | 10^7 |
| n^2 | 10^2 | 10^4 | 10^6 | 10^8 | 10^10 | 10^12 |
| n^3 | 10^3 | 10^6 | 10^9 | 10^12 | 10^15 | 10^18 |
| 2^n | 10^3 | 10^30 | 10^301 | 10^3,010 | 10^30,103 | 10^301,030 |

![](img/288a0c22d14d2450c1e772f228f867b0_323_0.png)

- 1. You can ignore low-order terms in an algorithm's growth-rate function. For example, if an algorithm is O(n^2 + 4n + 3), it is also O(n^2). By examining the table in Figure 10-3a, you can see that the n^2 term is significantly larger than either 4n or 3, particularly for large values of n. For large n, the growth rate of n^2 + 4n + 3 is the same as the growth rate of n^2. It is the growth rate of f(n), not the value of f(n), that is important here. Thus, even if an algorithm is O(n^2 + 4n + 3), we say that it is simply O(n^2). In general, you can usually conclude that an algorithm is O(f(n)), where f is a function similar to the ones listed in Figure 10-3.

## Some properties of growth-rate functions

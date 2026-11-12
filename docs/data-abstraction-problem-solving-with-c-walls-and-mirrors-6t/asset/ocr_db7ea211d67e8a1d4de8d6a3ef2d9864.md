# FIGURE 10-1 Time requirements as a function of the problem size n

![](bbox=[0.35, 0.13, 0.8, 0.35])

conclusion such as “A requires time proportional to n^2” is exactly the kind of statement that characterizes the inherent efficiency of an algorithm independently of such factors as particular computers and implementations.

Figure 10-1 also shows that A’s time requirement does not exceed B’s until n exceeds 25. Algorithm efficiency is typically a concern for large problems only. The time requirements for small problems are generally not large enough to matter. Thus, our analyses assume large values of n.

Note: When comparing the efficiency of various solutions, look only at significant differences. This rule is consistent with a multidimensional view of the cost of a computer program.

# 10.2.3 Analysis and Big O Notation

If Algorithm A requires time proportional to f(n)

Algorithm A is said to be order f(n), which is denoted as O(f(n)). The function f(n) is called the algorithm’s growth-rate function. Because the notation uses the capital letter O to denote order, it is called the Big O notation. If a problem of size n requires time that is directly proportional to n, the problem is O(n)—that is, order n. If the time requirement is directly proportional to n^2, the problem is O(n^2), and so on.

The following definition formalizes these ideas:

Note: Definition of the order of an algorithm Algorithm A is order f(n)—denoted O(f(n))—if constants k and n0 exist such that A requires no more than k x f(n) time units to solve a problem of size n >= n0.

The requirement n >= n0 in the definition of O(f(n)) formalizes the notion of sufficiently large problems. In general, many values of k and n can satisfy the definition.
# 3.7 ASYMPTOTIC NOTATION

Some of the algorithms may be short in the number of instructions but when input varies, the total number of execution steps grows gradually. The asymptotic notations will help to predict the program behavior at the runtime. It provides a measurable value. Using the asymptotic notations, the best algorithm can be found, which can perform better than the other possible algorithms of a problem. The asymptotic notations consider the operation count or step count of an algorithm.

# Example

Let A and B be the two algorithms for a problem where

```
A_n=3n^2+2n
B_n=5n
```

The computational growth of two algorithms varies with the n value as shown in Figure 3.1. In the graph, the x-axis represents the input variable values, i.e. n, and the y-axis represents the time complexity.

![](bbox=[0.18, 0.37, 0.75, 0.63])

Figure 3.1 Computational growth changes

Algorithms A and B work similarly with respect to the time complexities when n=1.

+   Time complexity of A=5 and
+   Time complexity of B=5
+   when n=2
+   Time complexity of A=16 and
+   Time complexity of B=10

Therefore, for n=2, B is the optimal algorithm.

Similar changes can be observed for other values of n as shown in the above graph.

# 3.7.1 Big oh Notation (O)

# Definition:

Let f(x) and g(x) be two non-negative functions defined on a set of real numbers. f(x) = O(g(x)) iff there exists positive constants ‘c’ and n0, such that f(n) <= cg(n) for all n >= n0,

The big oh notation considers the upper bound of the function.
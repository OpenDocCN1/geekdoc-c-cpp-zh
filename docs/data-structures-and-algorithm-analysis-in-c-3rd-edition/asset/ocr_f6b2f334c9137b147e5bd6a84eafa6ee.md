# 14.24 Use mathematical induction to prove that

∑_{i=1}^{n} Fib(i) = Fib(n+2) − 1, for n ≥ 1.

# 14.25 Use mathematical induction to prove that Fib(i) is even if and only if n is divisible by 3.

# 14.26 Use mathematical induction to prove that for n ≥ 6, fib(n) > (3/2)^{n−1}.

# 14.27 Find closed forms for each of the following recurrences.

+   (a) F(n) = F(n − 1) + 3; F(1) = 2.
+   (b) F(n) = 2F(n − 1); F(0) = 1.
+   (c) F(n) = 2F(n − 1) + 1; F(1) = 1.
+   (d) F(n) = 2nF(n − 1); F(0) = 1.
+   (e) F(n) = 2^{n}F(n − 1); F(0) = 1.
+   (f) F(n) = 2 + ∑_{i=1}^{n−1} F(i); F(1) = 1.

# 14.28 Find Θ for each of the following recurrence relations.

+   (a) T(n) = 2T(n/2) + n².
+   (b) T(n) = 2T(n/2) + 5.
+   (c) T(n) = 4T(n/2) + n.
+   (d) T(n) = 2T(n/2) + n².
+   (e) T(n) = 4T(n/2) + n³.
+   (f) T(n) = 4T(n/3) + n.
+   (g) T(n) = 4T(n/3) + n².
+   (h) T(n) = 2T(n/2) + log n.
+   (i) T(n) = 2T(n/2) + n log n.

# 14.6 Projects

# 14.1 Implement the UNION/FIND algorithm of Section 6.2 using both path compression and the weighted union rule. Count the total number of node accesses required for various series of equivalences to determine if the actual performance of the algorithm matches the expected cost of Θ(n log* n).
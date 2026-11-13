![](bbox=[0.31, 0.1, 0.79, 0.33])

Fig. 12.28 Binomial trees (c) Another way of looking at the binomial tree \( B_k \)

As shown in Fig. 12.28(a), the binomial tree \( B_0 \) consists of a single node.

For the binomial tree \( B_k \),

+   1. there are \( 2^k \) nodes
+   2. the height of the tree is \( k \)
+   3. there are exactly \( \binom{k}{i} \) nodes at depth \( i \) for \( i = 0, 1, ..., k \)
+   4. the root has degree \( k \), which is greater than that of any other node; moreover, if the children of the root are numbered from left to right by \( k-1, k-2, ..., 0 \), the child \( i \) is the root of a subtree

Always remember that the maximum degree of any node in \( n \)-node binomial tree is \( \log n \).

# 12.6.2 Binomial Heap

A binomial heap \( H \) is a set of binomial trees that satisfies the following binomial heap properties.

+   1. Each binomial tree in \( H \) follows the min-heap property. We say that each such tree is min-heap ordered.
+   2. For any non-negative integer \( k \), there is utmost one binomial tree in \( H \) whose root has degree \( k \).

Figure 12.29 shows an example of a binomial heap \( H \).

From Fig. 12.29, it is clear that the heap consists of three binomial trees \( B_0, B_1, B_2 \), and \( B_3 \). Since each binomial tree is min-heap-ordered, the key of any node is less than that of its parent. Also shown is the root list, which is a linked list of roots in the order of increasing degree.
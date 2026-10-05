# 530 Appendix B Solutions to Exercises

![](bbox=[0.125, 0.085, 0.814, 0.403])

**B-19:** Adding 11 values to an empty B-tree of order 2 makes the root node four children.

9. A B-tree of order K would occupy $1,024 \times (2 \times K) + 8 \times (2 \times K + 1) = 2,048 \times K + 16 \times K + 8 = 2,064 \times K$ bytes. To fit in four blocks of 2 KB each, this must be less than or equal to $4 \times 2 \times 1,024 = 8,192$ bytes, so $2,064 \times K + 8 \leq 8,192$. Solving for $K$ $K \leq (8,192-8) / 2,064$, or $K \leq 3.97. K$ must be an integer, so you must round this down to 3.

A B+-tree of order K would occupy $100 \times (2 \times K) + 8 \times (2 \times K + 1) = 200 \times K + 16 \times K + 8 = 216 \times K + 8$ bytes. To fit in four blocks of 2 KB each, this must be less than or equal to $4 \times 2 \times 1,024 = 8,192$ bytes, so $216 \times K + 8 \leq 8,192$. Solving for $K$ $K \leq (8,192-8) / 216$, or $K \leq 37.9. K$ must be an integer, so you must round this down to 37.

Each tree would have a height of $\log_{(K+1)}(10,000)$ while holding 10,000 items. For the B-tree, value is $\log_K(10,000) = 6.6$, so the tree could be seven levels tall. For the B+-tree, value is $\log_{2K}(10,000) = 2.5$, so the tree could be three levels tall.

# Decision12: Decision Trees

+   1. Example program CountTicToeBords does this. It found the following results:

+   - X won 131,184 times.

+   - O won 77,904 times.
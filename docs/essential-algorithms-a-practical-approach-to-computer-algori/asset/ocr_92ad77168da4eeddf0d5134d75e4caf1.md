# Appendix B = Solutions to Exercises 529

7. To remove the value 49 from the bottom tree in Figure B-17, simply replace the value 49 with the rightmost value to its left, which is 48. The node initially containing the 48 still holds three values, so it doesn't need to be rebalanced. Figure B-18 shows the result.

![](bbox=[0.187, 0.185, 0.859, 0.548])

Figure B-18: Sometimes when you remove a value, no rebalancing is required.

8. Figure B-19 shows a B-tree growing incrementally as you add the values 1 through 11. When you add 11, the root node has four children, so the tree holds 11 values at that point.
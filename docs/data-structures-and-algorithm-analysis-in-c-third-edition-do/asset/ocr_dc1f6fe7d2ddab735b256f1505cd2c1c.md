Sec. 7.9 Lower Bounds for Sorting

263

| XYZ | |
|---||
| XYZ YZX | |
| XZY ZXY | |
| XYZ ZYX | |
| Yes | A[1]<A[0]? (Y<X?) | No |
| YXZ | XYZ |
| YZX | XYZ |
| ZYX | ZXY |
| Yes | A[2]<A[1]? (Z<Y?) | No |
| YXZ | XZY |
| ZYX | ZXY |
| Yes | No | A[1]<A[0]? (Z<X?) | XYZ |
| ZYX (Z-Y?) | YXZ |

**Figure 7.21** Decision tree for Insertion Sort when three values labeled X, Y, and Z, initially stored at Insertions 0, 1, and 2, respectively, in input array.

compared and the first is less than the second, then this is modeled as a left branch in the decision tree. In the case where the first value is greater than the second, the algorithm takes the right branch.

Figure 7.21 shows the decision tree that models Insertion Sort on three input values. The first input value is labeled X, the second Y and the third Z. They are initially stored in positions 0, 1, and 2, respectively, of input array A. Consider the possible outputs. We know nothing about the final positions of the three values in the sorted order. The correct output could be any permutation of the input values. For three values, there are $n!=6$ permutations. Thus, the root of the decision tree lists all permutations that might be the eventual result of the algorithm.

When $n = 3$, the first comparison by Insertion Sort is the second item in the input array (Y) and the first item in the array (X). There are two possibilities: either the value of Y is less than that of X, or not less than X. This decision is modeled by the first branch. If Y is less than X, the left branch should be taken and Y must appear before X in the final output. Three of the original six permutations have this property, so the left child of the root lists the permutations where Y appears before X: XYZ, YZX, and ZYX. Likewise, if Y were not less than X, then the right branch would be taken, and only the three permutations in which Y appears after X are possible outcomes: XYZ, XZY, and ZXY. These are listed in the right child of the root.

Let us assume for the moment that Y is less than X and so the left branch is taken. In this case, Insertion Sort swaps the two values. At this point the array
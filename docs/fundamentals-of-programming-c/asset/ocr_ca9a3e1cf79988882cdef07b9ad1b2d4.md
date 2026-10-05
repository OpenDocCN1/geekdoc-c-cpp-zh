# 12.6. SUMMARY

first iteration of the for the leftmost 3-tuple represents the element at index zero swapped with the element at index zero (effectively no change). The second 3-tuple on the second row represents the interchange of the elements at index 0 and index 1. The third 3-tuple on the second row results from the interchange of the elements at positions 0 and 2. The underlined elements represent the most recently swapped. If only one in the 3-tuple is underlined, the function merely swapped the item with itself. The row of 3-tuples contains all the possible outcomes of the faulty_permute function given the vector (1, 2, 3).

As Figure 12.5 shows, the vector (1, 3, 2), (2, 1, 3), and (2, 3, 1) each appear five times in the last row, (1, 2, 3), (3, 1, 2), and (3, 2, 1) each appear four times. There $\frac{4}{5}$

are a total of 27 outcomes, some permutations appear $\frac{4}{27} = 14.815\%$ of the time, while the others appear $\frac{5}{27} = 18.519\%$ of the time. Notice that these percentages agree with our experimental results from Listing 12.9 (comparepermutations.cpp).

![](bbox=[0.298, 0.383, 0.755, 0.532])

Figure 12.6: A tree mapping out the ways in which permute can transform the vector 1, 2, 3 at each iteration of for loop

Compare Figure 12.5 to Figure 12.6. The second row of the tree for permute is identical to the second row of the tree for faulty_permute, but the third row is different. The second time its loop the permute function does not attempt to exchange the element at index zero with any other elements. We see that the first elements of the 3-tuples in three rows are underlined. The third row contains exactly one of each of the possible permutations of (1, 2, 3). This means that the correct permute function is not biased towards any of the individual permutations, and so the function can generate all the permutations with equal probability. The Permute function has a $\frac{1}{6}=16.667\%$ probability of generating a particular permutation; this number agrees with our experimental results of Listing 12.9 (comparepermutations.cpp).

# 12.6 Summary

+   * Various algorithms exist for sorting vectors. Selection sort is a simple algorithm for sorting a vector.
* Linear search is useful for finding elements in an unordered vector. Binary search can be used on ordered vectors, and due to the nature of the algorithm, binary search is very fast, even on large vectors.
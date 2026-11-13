Heapsort was invented by Williams [33]; Floyd [4] provided the linear-time algorithm for heap construction. Theorem 7.5 is from [23].

An exact average-case analysis of mergesort has been described in [7]. An algorithm to perform merging in linear time without extra space is described in [12].

Quicksort is from Hoare [10]. This paper analyzes the basic algorithm, describes most of the improvements, and includes the selection algorithm. A detailed analysis and empirical study was the subject of Sedgewick's dissertation [27]. Many of the important results appear in the three papers [24], [25], and [26]. [1] provides a detailed C implementation with some additional improvements, and points out that older implementations of the unix qsort library routine are easily driven to quadratic behavior. Exercise 7.27 is from [18].

Decision trees and sorting optimality are discussed in Ford and Johnson [5]. This paper also provides an algorithm that almost meets the lower bound in terms of number of comparisons (but not other operations). This algorithm was eventually shown to be slightly suboptimal by Manacher [17].

The selection lower bounds obtained in Theorem 7.9 are from [6]. The lower bound for finding the maximum and minimum simultaneously is from Pohl [21]. The current best lower bound for finding the median is slightly above 2N comparisons due to Dor and Zwick [3]; they also have the best upper bound, which is roughly 2.95N comparisons [2]. External sorting is covered in detail in [16]. Stable sorting, described in Exercise 7.31, has been addressed by Horvath [11].

+   1. J. L. Bentley and M. D. McIlroy, "Engineering a Sort Function," Software—Practice and Experience, 23 (1993), 1249–1265.
+   2. D. Dor and U. Zwick, "Selecting the Median," SIAM Journal on Computing, 28 (1999), 1722–1758.
+   3. D. Dor and U. Zwick, "Median Selection Requires (2 + ε)n Comparisons," SIAM Journal on Discrete Math, 14 (2001), 312–325.
+   4. R. W. Floyd, "Algorithm 245: Treesort 3," Communications of the ACM, 7 (1964), 701.
+   5. L. R. Ford and S. M. Johnson, "A Tournament Problem," American Mathematics Monthly, 66 (1959), 387–389.
+   6. F. Fussenegger and H. Gabow, "A Counting Approach to Lower Bounds for Selection Problems," Journal of the ACM, 26 (1979), 227–238.
+   7. M. Golin and R. Sedgewick, "Exact Analysis of Mergesort," Fourth SIAM Conference on Discrete Mathematics, 1988.
+   8. G. H. Gonnet and R. Baeza-Yates, Handbook of Algorithms and Data Structures, 2d ed., Addison-Wesley, Reading, Mass., 1991.
+   9. T. H. Hibbard, "An Empirical Study of Minimal Storage Sorting," Communications of the ACM, 6 (1963), 206–213.
+   10. C. A. R. Hoare, "Quicksort," Computer Journal, 5 (1962), 10–15.
+   11. E. C. Horvath, "Stable Sorting in Asymptotically Optimal Time and Extra Space," Journal of the ACM, 25 (1978), 177–199.
+   12. B. Huang and M. Langston, "Practical In-place Merging," Communications of the ACM, 31 (1988), 348–352.
+   13. J. Incerpt and R. Sedgewick, "Improved Upper Bounds on Shellsort," Journal of Computer and System Sciences, 31 (1985), 210–224.
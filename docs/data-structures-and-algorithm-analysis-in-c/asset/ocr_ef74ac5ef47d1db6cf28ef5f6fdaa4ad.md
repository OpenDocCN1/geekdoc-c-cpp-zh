+   a. In terms of R and C, which are the number of rows and columns in the puzzle, and W, which is the number of words, what are the running times of the algorithms described in Chapter 1?

+   b. Suppose the word list is presorted. Show how to use binary search to obtain an algorithm with significantly better running time.

+   2.31 Suppose that line 15 in the binary search routine had the statement `low = mid` instead of `low = mid + 1`. Would the routine still work?

+   2.32 Implement the binary search so that only one two-way comparison is performed in each iteration.

+   2.33 Suppose that lines 15 and 16 in algorithm 3 (Fig. 2.7) are replaced by
+   15 `int maxLeftSum = maxSumRec( a, left, center - 1 );`
+   16 `int maxRightSum = maxSumRec( a, center, right );`
+   Would the routine still work?

+   * 2.34 The inner loop of the cubic maximum subsequence sum algorithm performs N(N+1)(N+2)/6 iterations of the innermost code. The quadratic version performs N(N + 1)/2 iterations. The linear version performs N iterations. What pattern is evident? Can you give a combinatoric explanation of this phenomenon?

# References

Analysis of the running time of algorithms was first made popular by Knuth in the three-part series [5], [6], and [7]. Analysis of the gcd algorithm appears in [6]. Another early text on the subject is [1].

Big-Oh, big-omega, big-theta, and little-oh notation were advocated by Knuth in [8]. There is still no uniform agreement on the matter, especially when it comes to using $\Theta()$. Many people prefer to use O, even though it is less expressive. Additionally, O is still used in some corners to express a lower bound, when $\Omega()$ is called for.

The maximum subsequence sum problem is from [3]. The series of books [2], [3], and [4] show how to optimize programs for speed.

+   1. A. V. Aho, J. E. Hopcroft, and J. D. Ullman, *The Design and Analysis of Computer Algorithms*, Addison-Wesley, Reading, Mass., 1974.
+   2. J. L. Bentley, *Writing Efficient Programs*, Prentice Hall, Englewood Cliffs, N.J., 1982.
+   3. J. L. Bentley, *Programming Pearls*, Addison-Wesley, Reading, Mass., 1986.
+   4. J. L. Bentley, *More Programming Pearls*, Addison-Wesley, Reading, Mass., 1988.
+   5. D. E. Knuth, *The Art of Computer Programming, Vol 1: Fundamental Algorithms*, 3d ed., Addison-Wesley, Reading, Mass., 1997.
+   6. D. E. Knuth, *The Art of Computer Programming, Vol 2: Seminumerical Algorithms*, 3d ed., Addison-Wesley, Reading, Mass., 1998.
+   7. D. E. Knuth, *The Art of Computer Programming, Vol 3: Sorting and Searching*, 2d ed., Addison-Wesley, Reading, Mass., 1998.
+   8. D. E. Knuth, "Big Omicron and Big Omega and Big Theta," *ACM SIGACT News*, 8 (1976), 18–23.
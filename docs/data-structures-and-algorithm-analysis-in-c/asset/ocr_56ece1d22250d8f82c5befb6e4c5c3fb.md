7.3 Suppose we exchange elements a[i] and a[i+k], which were originally out of order. Prove that at least 1 and at most 2k - 1 inversions are removed.

7.4 Show the result of running Shellsort on the input 9, 8, 7, 6, 5, 4, 3, 2, 1 using the increments {1, 3, 7}.

+   7.5 a. What is the running time of Shellsort using the two-increment sequence {1, 2}?
+   b. Show that for any N, there exists a three-increment sequence such that Shellsort runs in O(N^(3/2)) time.
+   c. Show that for any N, there exists a six-increment sequence such that Shellsort runs in O(N^(3/2)) time.

+   7.6 * a. Prove that the running time of Shellsort is Omega(N^2) using increments of the form 1, c, c^2, ..., c^k for any integer c.
+   ** b. Prove that for these increments, the average running time is Theta(N^(3/2)).

** 7.7 Prove that if a k-sorted file is then h-sorted, it remains k-sorted.

** 7.8 Prove that the running time of Shellsort, using the increment sequence suggested by Hibbard, is Omega(N^(3/2)) in the worst case. (Hint: You can prove the bound by considering the special case of what Shellsort does when all elements are either 0 or 1.) Set a[i] = 1 if i is expressible as a linear combination of h_i, h_{i-1}, ..., h_floor(log2 N)+1 and 0 otherwise.

+   7.9 Determine the running time of Shellsort for
+   a. sorted input
+   * b. reverse-ordered input

+   7.10 Do either of the following modifications to the Shellsort routine coded in Figure 7.6 affect the worst-case running time?
+   a. Before line 8, subtract one from gap if it is even.
+   b. Before line 8, add one to gap if it is even.

7.11 Show how heapsort processes the input 142, 543, 123, 65, 453, 879, 572, 434, 111, 242, 811, 102.

7.12 What is the running time of heapsort for presorted input?

* 7.13 Show that there are inputs that force every percDown in heapsort to go all the way to a leaf. (Hint: Work backward.)

7.14 Rewrite heapsort so that it sorts only items that are in the range low to high, which are passed as additional parameters.

7.15 Sort 3, 1, 4, 1, 5, 9, 2, 6 using mergesort.

7.16 How would you implement mergesort without using recursion?

+   7.17 Determine the running time of mergesort for
+   a. sorted input
+   b. reverse-ordered input
+   c. random input

7.18 In the analysis of mergesort, constants have been disregarded. Prove that the number of comparisons used in the worst case by mergesort is N[ceil(log N)] - 2^(ceil(log N)) + 1.
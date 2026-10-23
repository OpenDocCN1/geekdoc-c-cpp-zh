# 18.10 SUMMARY AND CONCLUSIONS

In this chapter we have introduced *mutating, sorting, sorted range* and *numeric algorithms*. We provided complete machine-readable and machine-runnable code and corresponding output. We recommend that you do the exercises.

# 18.11 EXERCISES AND PROJECTS

1. (Choosing the Appropriate Algorithm Investigation)

Consider a general sequence container, for example `std::list` for convenience. This involves reading through Chapters 17 and 18 again. To which categories do the following algorithms belong and which specific algorithm would you use in each case? Determine what the output is in each case.

+   a) Scale all values by a given factor.
+   b) Count the number of elements whose values are in a given range.
+   c) Find the average, minimum and maximum values in a container.
+   d) Find the first element that is (is not) in a range.
+   e) Search for all occurrences of ‘3456’ in the container.
+   f) Determine if the elements of two ranges are equal.
+   g) Determine if a set is some permutation of ‘12345’.
+   h) Is a container already sorted?
+   i) Copy a container into another container.
+   j) Move the last 10 elements of a container to the front of the container.
+   k) Swap two ranges at a given position.
+   l) Generate values in a container based on some formula.
+   m) Replace all uneven numbers by zero.
+   n) Remove all elements whose value is less than 100.
+   o) Shuffle a container randomly using both pre- and post-C++11 versions.
+   p) Compute one-sided divided differences of the values in a container.

Now take specific containers, for example `std::vector`, and implement each of the above operations. The challenge here lies in finding the most appropriate STL algorithm to use and then implementing it.

For each of the above questions a) to p) ask yourself the following questions:

+   What is algorithm input? What is the output?
+   Is the input modified on output?
+   Which category does the algorithm belong to?
+   Choose the most appropriate algorithm and implement it.
+   Check and understand the output.
+   Think about the process of producing output from input.
+   Think about (other examples) where you can use the algorithm.

You will know that you have successfully completed the exercises when you have executed these steps. Understand the output. After having completed these exercises you will have gained a good understanding of STL algorithms for sure.

2. (Priority Queue)

In this exercise we create a *priority queue* that is supported in STL:
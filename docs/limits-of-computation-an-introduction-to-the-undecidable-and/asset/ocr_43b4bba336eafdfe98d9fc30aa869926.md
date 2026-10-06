# Limits of Computation

2). To fill row i, table[i,j] is true if either (1) the entry above it is true or
(2) the entry in the row above that is Ij to the left is true; that is, table[i−1,
j−Ij] = true. By hand, the easiest way to proceed is to (1) copy all T's from
the previous row down to the current row, and (2) add Ij to each entry thatnhas a true in the row above, and if not already true in this row, make it.

To demonstrate, consider filling in the third row (labeled 6 Ij = 6).
Copy the four true's from the previous row (0, 2, 3, 5). Then 6 = 0 + 0,
8 = 2 + 6, 9 = 3 + 6, and 11 = 5 + 6 also becomes true.
there are only n(T+1) entries, and each requires
one one addition, the algorithm is polynomial in T.

The input consists of the n numbers ... In and the one number T.
At glance, the size of the input is (n + 1) and the algorithm is poly-
nomial. However, the reader should be suspicious, this problem is
NP-complete.

What is going on? The answer is that the size of the input depends on
the size of the numbers ... Each number I requires log₀(I)
to represent it in decimal, T requires log₀ T. We can assume that T
larger than any of the ... If it is not, any of the I, are larger than T
be discarded as they can play no part in the Subset Sum. This good
bound for the size of the input is (n log₀ T), and nT is not polynomial in
this quantity.

We now try to capture what is going on the easy algorithm for PRIME
d the dynamic programming algorithm for Subset Sum. These algo-ithms are very slow if the size of the integers in the input is large. If
all input numbers were bounded to fit in a long-length integer on a stan-
dard computer, the problem would be much easier. The idea is to capture
difficulty arising because there are unboundedly large numbers in the
problem, and it is the size of these integers that makes the problem difficult.

# Definition 10.1

A decision problem is a number problem if there is no polynomial bound
on the largest number that is part of the problem input, in terms of the
length of the encoding of the input.

Let Max(input) be the size of the largest number in an instance I of a
problem A (if A has no numbers, Max(input) = 0). The size of the input
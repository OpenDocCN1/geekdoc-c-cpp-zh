Unfortunately, for many applications this is not what the user wants or expects. For example, many hash systems will perform some computation on a record’s key value and then take the result modulo the hash table size. The expectation here would be that the result is a legal index into the hash table, not a negative number. Implementers of hash functions must either insure that the result of the computation is always positive, or else add the hash table size to the result of the modulo function when that result is negative.

# 2.3 Logarithms

A logarithm of base b for value y is the power to which b is raised to get y. Normally, this is written as log_b y = x. Thus, if log_b y = x then b^x = y, and b^{log_b y} = y.

Logarithms are used frequently by programmers. Here are two typical uses.

Example 2.6 Many programs require an encoding for a collection of objects. What is the minimum number of bits needed to represent n distinct code values? The answer is ⌈log₂ n⌉ bits. For example, if you have 1000 codes to store, you will require at least ⌈log₂ 1000⌉ = 10 bits to have 1000 different codes (10 bits provide 1024 distinct code values).

Example 2.7 Consider the binary search algorithm for finding a given value within an array sorted by value from lowest to highest. Binary search first looks at the middle element and determines if the value being searched for is in the upper half or the lower half of the array. The algorithm then continues splitting the appropriate subarray in half until the desired value is found. (Binary search is described in more detail in Section 3.5.) How many times can an array of size n be split in half until only one element remains in the final subarray? The answer is ⌈log₂ n⌉ times.

In this book, nearly all logarithms used have a base of two. This is because data structures and algorithms most often divide things in half, or store codes with binary bits. Whenever you see the notation log n in this book, either log₂ n is meant or else the term is being used asymptotically and so the actual base does not matter. Logarithms using any base other than two will show the base explicitly.

Logarithms have the following properties, for any positive values of m, n, and r, and any positive integers a and b.

+   1. log(nm) = log n + log m.
+   2. log(n/m) = log n − log m.
+   3. log(n^r) = r log n.
+   4. log_a n = log_b n / log_b a.
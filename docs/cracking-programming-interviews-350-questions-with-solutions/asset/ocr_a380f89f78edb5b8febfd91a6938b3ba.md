# Chapter 6

# Miscellaneous

# 6.1 Compute Next Higher Number

# Problem

Compute the next higher number of a given integer using the same digits. It is also know as *next higher permutation* of a given number.

# Solution

Let us assume that such a permutation exists and *n* be the number of digits of the array *a*. Let us take an example to understand this problem closely. Let the input integer sequence be:

`{1, 2, 3, 5, 4, 2}`

Here n = 6. We observe the following property for index i = 2:

+   - a[2] = 3 < 5 = a[3], i.e., a[i] < a[i + 1]
+   - 5, 4, 2 is a non-increasing sequence, i.e., a[i + 1 ... n - 1] is non-increasing
+   - 4 is the smallest value of the sequence 5, 4, 2 which is greater than 3 such that the immediate next value (2) is less than 3. Let us denote this index as j(4), i.e., a[j] = 4 and a[j + 1] = 3 < a[i].
+   - Hence the next permutation can be achieved by swapping a[i] with a[j]. ⇒ 1, 2, 4, 5, 3, 2 is a higher permutation than the original sequence.
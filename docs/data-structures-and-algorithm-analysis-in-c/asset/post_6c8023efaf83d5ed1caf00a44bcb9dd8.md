
![](img/e449061a0cac9cafaefd979fab665b33_602_0.png)

trie in Figure 12.25 is exactly one less than the number of internal branching nodes in the original trie in Figure 12.25. And of course writing all the suffixes in the leaves could take quadratic space. So if the original used quadratic space, so does the compressed trie. Fortunately, we can get by with linear space as follows:

- 1. In the leaves, we use the index where the suffix begins (as in the suffix array).
- 2. In the internal nodes, we store the number of common characters matched from the root until the internal node; this number represents the letter depth.

![](img/e449061a0cac9cafaefd979fab665b33_602_1.png)

The internal node with a letter depth of 1 is representing the common string "a" in all nodes that are below it. The internal node with a letter depth of 3 is representing the common string "ana" in all nodes that are below it. And the internal node with a letter depth of 2 is representing the common string "na" in all nodes that are below it. In fact, this analysis makes clear that a suffix tree is equivalent to a suffix array plus an LCP array.

If we have a suffix tree, we can compute the suffix array and the LCP array by performing an inorder traversal of the tree (compare Figure 12.23 with the suffix tree in Figure 12.26). At that time we can compute the LCP as follows: If the suffix node value PLUS the letter depth of the parent is equal to N, then use the letter depth of the grandparent as the LCP; otherwise use the parent's letter depth as the LCP. In Figure 12.26, if we proceed inorder, we obtain for our suffixes and LCP values

- Suffix = 5, with LCP = 0 (the grandparent) because 5 + 1 equals 6
- Suffix = 3, with LCP = 1 (the grandparent) because 3 + 3 equals 6
- Suffix = 1, with LCP = 3 (the parent) because 1 + 3 does not equal 6
- Suffix = 0, with LCP = 0 (the parent) because 0 + 0 does not equal 6
- Suffix = 4, with LCP = 0 (the grandparent) because 4 + 2 equals 6
- Suffix = 2, with LCP = 2 (the parent) because 2 + 2 does not equal 6

This transformation can clearly be done in linear time.

The suffix array and LCP array also uniquely define the suffix tree. First, create a root with letter depth 0. Then search the LCP array (ignoring position 0, for which LCP is not really defined) for all occurrences of the minimum (which at this phase will be the zeros). Once these minimums are found, they will partition the array (view the LCP as residing between adjacent elements). For instance, in our example, there are two zeros in the LCP array, which partitions the suffix array into three portions: one portion containing the suffixes (5, 3, 1), another portion containing the suffix (0), and the third portion containing the suffixes (4, 2). The internal nodes for these portions can be built recursively, and then the suffix leaves are attached with an inorder traversal. Although it is not obvious, with care the suffix tree can be generated in linear time from the suffix array and LCP array

The suffix tree solves many problems efficiently, especially if we augment each internal node to also maintain the number of suffixes stored below it. A small sampling of suffix tree applications includes the following:

- 1. Find the longest repeated substring in T: Traverse the tree, finding the internal node with the largest number letter depth; this represents the maximum LCP. The running time is O(| T | ). This generalizes to the longest substring repeating at least k times.
- 2. Find the longest common substring in two strings T1 and T2: Form a string T1#T2 where # is a character that is not in either string. Then build a suffix tree for the resulting string and find the deepest internal node that has at least one suffix that starts prior to the #, and one that starts after the #. This can be done in time proportional to the total size of the strings and generalizes to an O(k n) algorithm for k strings of total length N.
- 3. Find the number of occurrences of the pattern P: Assuming that the suffix tree is augmented so that each node keeps track of the number of suffixes below it, simply follow the path down the tree; the first internal node that is a prefix of P provides the answer; if there is no such node, the answer is either zero or one and is found by checking the suffix at which the search terminates. This takes time, proportional to the length of the pattern P, and is independent of the size of |T|.
- 4. Find the most common substring of a specified length L > 1: Return the internal node with largest size amongst those with letter depth at least L. This takes time O(|T|).

## 12.4.3 Linear-Time Construction of Suffix Arrays and Suffix Trees

In Section 12.4.1 we showed the simplest algorithm to construct a suffix array and an LCP array, but this algorithm has O(N^2 log N) worst-case running time for an N-character string and can occur if the string has suffixes with long common prefixes. In this section we describe an O(N) worst-case time algorithm to compute the suffix array. This algorithm can also be enhanced to compute the LCP array in linear time, but there is also a very simple linear-time algorithm to compute the LCP array from the suffix array (see Exercise 12.2-9 and complete code in Fig. 12.49). Either way, we can thus also build a suffix tree in linear time.

This algorithm makes use of divide and conquer. The basic idea is as follows:

- 1. Choose a sample, A, of suffixes.
- 2. Sort the sample A by recursion.
- 3. Sort the remaining suffixes, B, by using the now-sorted sample of suffixes A.
- 4. Merge A and B.

To get an intuition of how step 3 might work, suppose the sample A of suffixes are all suffixes that start at an odd index. Then the remaining suffixes, B, are those suffixes that start at an even index. So suppose we have computed the sorted set of suffixes A. To compute the sorted set of suffixes B, we would in effect need to sort all the suffixes that start at even indices. But these suffixes each consist of a single first character in an even position, followed by a string that starts with the second character, which must be in an odd position. Thus the string that starts in the second character is exactly a string that is in A. So to sort all the suffixes B, we can do something similar to a radix sort: First sort the strings in B starting from the second character. This should take linear time, since the sorted order of A is already known. Then stably sort on the first character of the strings in B. Thus B could be sorted in linear time, after A is sorted recursively. If A and B could then be merged in linear time, we would have a linear-time algorithm. The algorithm we present uses a different sampling step, that admits a simple linear-time merging step.

As we describe the algorithm, we will also show how it computes the suffix array for the string ABRACADABRA. We adopt the following conventions:

| S[i] | represents the ith character of string S |
|---|---|
| S[i -> ] | represents the suffix of S starting at index i |
| <-> | represents an array |

Step 1: Sort the characters in the string, assigning them numbers sequentially starting at 1. Then use those numbers for the remainder of the algorithm. Note that the numbers that are assigned depend on the text. So, if the text contains DNA characters A, C, G, and T only, then there will be only four numbers. Then pad the array with three 0s to avoid boundary cases. If we assume that the alphabet is a fixed size, then the sort takes some constant amount of time.

### Example:

In our example, the mapping is A = 1, B = 2, C = 3, D = 4, and R = 5; the transformation can be visualized in Figure 12.27.

### Step 2: Divide the text into three groups:

```
S0 = < S[3i]S[3i + 1]S[3i + 2] for i = 0, 1, 2, ... >
S1 = < S[3i + 1]S[3i + 2]S[3i + 3] for i = 0, 1, 2, ... >
S2 = < S[3i + 2]S[3i + 3]S[3i + 4] for i = 0, 1, 2, ... >
```

The idea is that each of S0, S1, S2 consists of roughly N/3 symbols, but the symbols are no longer the original alphabet, but instead each new symbol is some group of three symbols from the original alphabet. We will call these tri-characters. Most importantly, the suffixes of S0, S1, and S2 combine to form the suffixes of S. Thus one idea would be to recursively compute the suffixes of S0, S1, and S2 (which by definition implicitly represent sorted strings) and then merge the results in linear time. However, since this would be three recursive calls on problems 1/3 the original size, that would result in an O( N log N ) algorithm. So the idea is going to be to avoid one of the three recursive calls, by computing two of the suffix groups recursively and using that information to compute the third suffix group.

### Example:

In our example, if we look at the original character set and use $ to represent the padded character, we get

```
S0 = [ABR], [ACA], [DAB], [RA$]
S1 = [BRA], [CAD], [ABR], [A$$]
S2 = [RAC], [ADA], [BRA]
```

We can see that in S0, S1, and S2, each tri-character is now a trio of characters from the original alphabet. Using that alphabet, S0 and S1 are arrays of length four and S2 is an

| Input String, S | A | B | R | A | C | A | D | A | B | R | A | | | |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| New Problem | 1 | 2 | 5 | 1 | 3 | 1 | 4 | 1 | 2 | 5 | 1 | 0 | 0 | 0 |
| Index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 |

Figure 12.27 Mapping of character in string to an array of integers

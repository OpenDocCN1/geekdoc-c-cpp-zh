
| | - | A | G | C | A | T | G | C |
|---|---|---|---|---|---|---|---|---|
| - | 0 | -1 | -2 | -3 | -4 | -5 | -6 | -7 |
| A | -1 | 2 | 1 | 0 | -1 | -2 | -3 | -4 |
| C | -2 | 1 | 1 | 3 | 2 | 1 | 0 | -1 |
| A | -3 | 0 | 0 | 2 | 5 | 4 | 3 | 2 |
| A | -4 | -1 | -1 | 1 | 4 | 4 | 3 | 2 |
| T | -5 | -2 | -2 | 0 | 3 | 6 | 5 | 4 |
| C | -6 | -3 | -3 | 2 | 2 | 5 | 5 | 7 |
| C | -7 | -4 | -4 | -1 | 1 | 4 | 4 | 7 |

Figure 6.1: String Alignment Example for A = ‘ACAATCC’ and B = ‘AGCATGC’ (score = 7)

In Figure 6.1, the alignment score is 7 (bottom right). Follow the dashed (red) arrows from the bottom right cell to reconstruct the solution. Diagonal arrow means a match or a mismatch (e.g. the last ‘C’). Vertical arrow means a deletion (e.g. ..CAT.. to ..C_A_..). Horizontal arrow means an insertion (e.g. A_C.. to AGC..).

```
A = ‘A_CAAT[C]C’
B = ‘AGC_AT[G]C’
```

As we need to fill in all entries in the table of n × m matrix and each entry can be computed in O(1), the time complexity is O(nm). The space complexity is O(nm) – the size of the DP table.

### 6.3.2 Longest Common Subsequence

The Longest Common Subsequence (LCS) problem is defined as follows: Given two strings A and B, what is the longest common subsequence between them. For example, A = ‘ACAATCC’ and B = ‘AGCATGC’ have LCS of length 5, i.e. ‘AGATC’.

The LCS solution is very similar to String Alignment solution presented earlier. Set the cost for mismatch as negative infinity, cost for insertion and deletion as 0, and the cost for match as 1. This makes the String Alignment solution never consider mismatches.

### 6.3.3 Palindrome

A palindrome is a string that can be read the same way in either direction. Some variants of palindrome finding problems are solvable with DP technique, as shown in this example: given a string of up to 1000 characters, determine the length of the longest palindrome that you can make from it by deleting zero or more characters. Examples:

- ‘ADAM’ → ‘ADA’ (of length 3, delete ‘M’)
- ‘MADAM’ → ‘MADAM’ (of length 5, delete nothing)
- ‘NEVERODDOREVENING’ → ‘NEVERODDOREVEN’ (of length 14, delete ‘ING’)

The DP solution: let len(l, r) be the length of the longest palindrome from string A[l ... r].

```
Base cases:
If (l = r), then len(l, r) = 1. // true in odd-length palindrome
If (l + 1 = r), then len(l, r) = 2 if (A[l] = A[r]), or 1 otherwise. // true in even-length palindrome
```

Recurrences:
If \(A[l] = A[r]\), then \(len(l,r) = 2 + len(l+1,r-1)\).  // both corner characters are similar
else \(len(l,r) = max(len(l,r-1), len(l+1,r))\).  // increase left side or decrease right side

Programming Exercises related to String Processing with DP:

- 1. UVa 164 - String Computer (String Alignment/Edit Distance)
- 2. UVa 531 - Compromise (Longest Common Subsequence + printing solution)
- 3. UVa 10066 - The Twin Towers (Longest Common Subsequence - but not on ‘string’)
- 4. UVa 10100 - Longest Match (Longest Common Subsequence)
- 5. UVa 10192 - Vacation (Longest Common Subsequence)
- 6. UVa 10405 - Longest Common Subsequence (as the problem name implies)
- 7. UVa 10739 - String to Palindrome
- 8. UVa 11151 - Longest Palindrome
- 9. LA 2460 - Searching Sequence Database in Molecular Biology (String Alignment)

## 6.4 Suffix Tree and Suffix Array

Suffix Tree and Suffix Array are two efficient and related data structures for strings. We do not put this topic in Chapter 2 as these two data structures are special for strings.

### 6.4.1 Suffix Tree: Basic Ideas

![](img/2f3eff2c1d9ecd727dd36c1db12a8ec9_125_0.png)

Figure 6.2: Suffix Trie (Left) and Suffix Tree (Right) of S = ’acacag$’ (Figure from [24])

Consider a string² S = ’acacag$’, a Suffix³ Trie of S is a tree that contains all possible suffixes of S (see Figure 6.2, left). Two suffixes that share common prefix will share the same first few vertices, e.g. ’cag$’ and ’cacag$’ share the first two vertices ’ca’ before they split. The leaves contain the indices of the suffixes. Suffix Tree of S is Suffix Trie where we merge vertices with only one child (see Figure 6.2, right). Notice the ‘edge-label’ and ‘path-label’ in the figure.

Exercise: Draw the Suffix Tree of S = ’competitive$’!

² Notice that S is usually appended with a special char ‘$’ which is lexicographically smaller than all the alphabets used in S.

³ A suffix of a string is a ‘special case’ substring that goes up to the last character of the string.

### 6.4.2 Applications of Suffix Tree

Assuming that a Suffix Tree⁴ for a string $S$ is already built, we can use it for these applications:

**Exact String Matching in $O(|Q| + occ)$**

With Suffix Tree, we can find all (exact) occurrences of a query string $Q$ in $S$ in $O(|Q|+occ)$ where $|Q|$ is the length of the query string $Q$ itself and $occ$ is the total number of occurrences of $Q$ in $S$ — no matter how long the string $S$ is. When the Suffix Tree is already built, this approach is *faster* than many exact string matching algorithms (e.g. KMP).

With Suffix Tree, our task is to search for the vertex $x$ in the Suffix Tree which represents the query string $Q$. This can be done by just one root to leaf traversal that follows the edge labels. Vertex with path-label $= Q$ is the desired vertex $x$. Then, leaves in the subtree rooted at $x$ are the occurrences of $Q$ in $S$. We can then read the starting indices of such substrings that are stored in the leaves of the subtree.

For example, in the Suffix Tree of $S = ’acacag$’$ shown in Figure 6.2, right, and $Q = ’aca’$, we can simply traverse from root, go along the edge label ‘a’, then the edge label ‘ca’ to find vertex $x$ with the path-label ‘aca’ (follow the dashed red arrow in Figure 6.2, right). The leaves of this vertex $x$ point to index 1 (substring: ’acacag$’) and index 3 (substring: ’acag$’).

Exercise: Now try to find a query string $Q = ’ca’$ and $Q = ’cat’$!

**Finding Longest Repeated Substring in $O(n)$**

With Suffix Tree, we can also find the longest repeated substring in $S$ easily. The deepest internal vertex $X$ in the Suffix Tree of $S$ is the answer. Vertex $X$ can be found with an $O(n)$ tree traversal. The fact that $X$ is an internal vertex implies that it represents more than one suffix (leaves) of string $S$ and these suffixes share a common prefix (repeated substring). The fact that $X$ is the deepest internal vertex (from root) implies that its path-label is the longest repeated substring.

For example, in the Suffix Tree of $S = ’acacag$’$ shown in Figure 6.2, right, the longest repeated substring is ‘aca’ as it is the path-label of the deepest internal vertex.

Exercise: Find the longest repeated substring in $S = ’cgacattacatta$’!

**Finding Longest Common Substring in $O(n)$**

The problem of finding the Longest Common Substring (not Subsequence)⁵ of two or more strings can be solved in linear time with Suffix Tree. Consider two strings $S1$ and $S2$; we can build a generalized Suffix Tree for $S1$ and $S2$ with two different ending markers, e.g. $S1$ with character ‘#’ and $S2$ with character ‘$’. Then, we mark each internal vertex that has leaves that represent suffixes of both $S1$ and $S2$ – this means the suffixes share a common prefix. We then report the deepest marked vertex as the answer.

For example, with $S1 = ’acgath#$’$ and $S2 = ’cgt$’$, the Longest Common Substring is ’cg’ of length 2. In Figure 6.3, we see the root and vertices with path-labels ‘cg’, ‘g’, and ‘t’ all have two different leaf markers. The deepest marked vertex is ‘cg’. The two suffixes $cgat#$ and $cgt$ share a common prefix ‘cg’.

![](img/2f3eff2c1d9ecd727dd36c1db12a8ec9_127_0.png)

Exercise: Find the Longest Common Substring of S1 = 'steven$' and S2 = 'seven$'!

### 6.4.3 Suffix Array: Basic Ideas

Building efficient Suffix Tree under contest environment is a bit complex and risky. Fortunately, another data structure that we are going to describe, called Suffix **Array**, invented by Udi Manber and Gene Myers, has similar functionalities as Suffix Tree but simpler to implement, especially in programming contest settings. Thus we will skip the discussion on building a Suffix Tree and instead focus on Suffix Array.

Basically, Suffix Array is an integer array that contains indices of sorted suffixes. For example, consider the same S = 'acacag$' with *n* = 7. The Suffix Array of S is an integer permutation of *n* as shown in Figure 6.4. Note that we regard the terminating symbol $ as the lexicographically smallest character.

| Suffix | Position |
|---|---|
| acacag$ | 1 |
| cacag$ | 2 |
| acag$ | 3 |
| cag$ | 4 |
| ag$ | 5 |
| g$ | 6 |
| $ | 7 |

⇒ Sort

| SA[i] | Suffix |
|---|---|
| 7 | $ |
| 1 | acacag$ |
| 3 | acag$ |
| 5 | ag$ |
| 2 | cacag$ |
| 4 | cag$ |
| 6 | g$ |

Figure 6.4: Suffix Array of S = 'acacag$' (Figure from [24])

Suffix Tree and Suffix Array are very related. As we can see in Figure 6.5, the leaves of a Suffix Tree (from left to right) are in Suffix Array order. In short, a **vertex** in Suffix Tree corresponds to a **range** in Suffix Array!

![](img/2f3eff2c1d9ecd727dd36c1db12a8ec9_127_1.png)

A Suffix Array is good enough for many practical string operations in contest problems. In this section, we present two simple ways to build a Suffix Array given a string S[0 . . . n-1].

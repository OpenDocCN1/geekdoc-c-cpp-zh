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

in Figure 6.1. The alignment score is 7 (bottom right). Follow the dashed (red) arrows from the bottom right cell to reconstruct the solution. Diagonal arrow means a match or a mismatch (e.g. the last ‘C’). Vertical arrow means a deletion (e.g. ..CAT.. to ..C_A_..). Horizontal arrow means an insertion (e.g. A_C.. to AGC..).

```
`A = ‘A_CAAT[C]C’`
`B = ‘AGC_AT[G]C’`
```

As we need to fill in all entries in the table of n × m matrix and each entry can be computed in O(1), the time complexity is O(nm). The space complexity is O(nm) – the size of the DP table.

# ### 6.3.2 Longest Common Subsequence

The Longest Common Subsequence (LCS) problem is defined as follows: Given two strings A and B, what is the longest common subsequence between them. For example, A = ‘ACAATCC’ and B = ‘AGCATGC’ have LCS of length 5, i.e. ‘AGATC’.

The LCS solution is very similar to String Alignment solution presented earlier. Set the cost for mismatch as negative infinity, cost for insertion and deletion as 0, and the cost for match as 1. This makes the String Alignment solution to never consider mismatches.

# ### 6.3.3 Palindrome

A palindrome is a string that can be read the same way in either direction. Some variants of palindrome finding problems are solve-able with DP technique, as shown in this example: given a string of up to 1000 characters, determine the length of the longest palindrome that you can make from it by deleting zero or more characters. Examples:

+   - ‘ADAM’ → ‘ADA’ (of length 3, delete ‘M’)
+   - ‘MADAM’ → ‘MADAM’ (of length 5, delete nothing)
+   - ‘NEVERODDOREVENING’ → ‘NEVERODDOREVEN’ (of length 14, delete ‘ING’)

The DP solution: let len(l, r) be the length of the longest palindrome from string A[l ... r].

```
`Base cases:`
`If (l = r), then len(l, r) = 1. // true in odd-length palindrome`
`If (l + 1 = r), then len(l, r) = 2 if (A[l] = A[r]), or 1 otherwise. // true in even-length palindrome`
```
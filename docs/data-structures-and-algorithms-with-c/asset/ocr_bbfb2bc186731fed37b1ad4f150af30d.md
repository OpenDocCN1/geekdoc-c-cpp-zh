Now, T is shifted one position right

![](bbox=[0.35, 0.1, 0.65, 0.15])

no match

Again, T is shifted one position right

![](bbox=[0.35, 0.22, 0.65, 0.27])

match

Pattern string P is a substring of text string S

# Figure 3.19: String matching

# Brute Force (Naive) string matching algorithm

```
Algorithm: STRING_MATCHING (S, P)
[S is a text string and P is a pattern string]
1. Set N = Length (S)
2. Set M = Length (P)
3. Repeat For I = 0 to N-M do
4.   Set J = 0
5.   Repeat while J < M and S[I + J] = P[J] do
6.     Set J = J + 1
7.     If J >= M Return I
   [End of Loop]
[End of Loop]
8. Return -1
```

In the above algorithm, the for-loop is executed at most n - m + 1 times and the while loop are executed at most m times. Therefore, in the worst case, the running time complexity of this algorithm is O ((n - m + 1) m), which is O (nm), if n<<m. Consider an example where searching for a pattern like "xxxxx" in a string like "xxxxxxxy". In the average case, the running time complexity of this algorithm is O(m + n).

The advantage of this algorithm that it is a very simple technique and that does not require any pre-processing. Therefore, total running time is the same as its matching time. Although, it is a very inefficient method. Because this method takes only one position movement in each time.

In C language, the strstr() function finds the first occurrence of a substring in another string. On success, strstr() returns a pointer to the element in str1 where str2 begins (points to str2 in str1). On error (if str2 does not occur in str1), strstr() returns null. The general form of strstr() function is

```
ptr = strstr(str1, str2);
```
+   - Delete part of a string.
+   - Modify and compare strings in other ways.

The following is a set of operations we might want to do on strings.

| Operation | Description |
|---|---|
| GETCHAR(str, n) | Returns the n<sup>th</sup> character in the string |
| PUTCHAR(str, n, c) | Sets the n<sup>th</sup> character in the string to c |
| LENGTH(str) | Returns the number of characters in the string |
| POS(str1, str2) | Returns the position of the first occurrence of str2 found in str1, or 0 if no match |
| CONCAT(str1, str2) | Returns a new string consisting of characters in str1 followed by characters in str2 |
| SUBSTRING(str1, i, m) | Returns a substring of length m starting at position i in string str |
| DELETE(str, i, m) | Deletes m characters from str starting at position i |
| INSERT(str1, str2, i) | Changes str1 into a new string with str2 inserted in position i |
| COMPARE(str1, str2) | Returns an integer indicating whether str1 > str2 |

Let S1 be a string. There are a number of ways in which this string can be implemented as shown in Example 3.3.

> **Example 3.3**
> 
> Suppose S1 = ‘JANICE’.
> 
> (a) In this case, as the length is known, it can be implemented as a fixed length array, where the first element denotes the length of the string as shown below.
> 
> [6, J, A, N, I, C, E]
> 
> (b) If the length is not known, it can be implemented as an array but with the end of the string indicated using a special ‘NULL’ character denoted by ‘\0’ as shown below. Memory can then be dynamically allocated for the string once we know its length.
> 
> [J, A, N, I, C, E, \0,.....]
> 
> The first implementation has the disadvantages of all fixed length array implementations. However, some operations are efficient, for instance, finding the length.
> 
> The second implementation has the advantages of dynamic allocation of space; modifying the string also may be more efficient, as we need not recalculate size.

# 3.6 STRING OPERATIONS

Although a string may be viewed simply as a sequence or linear array of characters, there is a fundamental difference in use between strings and other types of arrays. Specifically, groups of consecutive elements in a string (such as words, phrases and sentences), called substrings, may be units unto themselves. Furthermore, the basic units of access in a string are usually these substrings, not individual characters.

Consider, for example, the string

```
'TO BE OR NOT TO BE'
```

We may view the string as the 18-character sequence T, O, □, B, ..., E. However, the substrings TO, BE, OR, ... have their own meaning.

On the other hand, consider an 18-element linear array of 18 integers,
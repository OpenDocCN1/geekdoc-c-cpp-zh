a prefix expression and Y is any nonempty string of nonblank characters, then E Y cannot be a prefix expression. This is a subtle point; Exercise 17 at the end of this chapter asks you to prove it.

If E is a prefix expression, E Y cannot be

Given this observation, you can begin to determine whether you have two consecutive prefix expressions by observing a first prefix expression. If you find one, the previous observation implies that only one endpoint is possible for this first expression.

If you find that the first prefix expression ends at position end1, you then attempt to find a second prefix expression beginning at position end1 + 1. If you find the second expression, you must check whether you are at the end of the string in question.

By using these ideas, you can show, for example, that +*ab-cd is a prefix expression. For +*ab-cd to be a prefix expression, it must be of the form +E1E2, where E1 and E2 are prefix expressions. Now you can write

+   E1 = * E2 E4, where
+   E2 = a
+   E4 = b

Because E1 and E4 are prefix expressions, E1 is a prefix expression. Similarly, you can write

+   E2 = - E5 E6, where
+   E3 = c
+   E6 = d

and you see that E2 is a prefix expression.

You can write a function to test whether an expression is a prefix expression by first constructing a recursive valued function endPre(strExp, first) to examine the expression that begins at position first of the string strExp and to locate the end of the first prefix expression it finds. If successful, the function returns the index of the end of the prefix expression. If no such prefix expression exists, endPre returns -1. The function appears in pseudocode as follows.

endPre determines the end of a prefix expression

```
// Finds the end of a prefix expression, if one exists.
// Precondition: The substring of strExp from the index first through the end of
// the string contains no blank characters.
// Postcondition: Returns the index of the last character in the prefix expression that
// begins at index first of strExp, or -1 if no such prefix expression exists.
endPre(strExp: string, first: integer): integer
last = strExp.length() - 1
if (first < 0 or first > last)
return -1
ch = character at position first of strExp
if (ch is an identifier)
return first // Index of last character in simple prefix expression
else if (ch is an operator)
{
// Find the end of the first prefix expression
firstEnd = endPre(strExp, first + 1) // Point X
// If the end of the first prefix expression was found, find the end of the second
// prefix expression
if (firstEnd > -1)
return endPre(strExp, firstEnd + 1) // Point Y
else
return -1
}
else
return -1
```
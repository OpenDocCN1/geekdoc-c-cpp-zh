# 9.4 String Library Functions

cases there is another form of the string compare function. This function has three arguments. The following example shows the use of such a function.

```
strng1[] = "comparison";
strng2[] = "communication";
```

| c | o | m | p | a | r | i | s | o | n | \0 |

```
k = strncmp(strng1, strng2, n);
```

| c | o | m | m | u | i | c | a | t | i | o | n | \0 |

Where n is the number of characters from the beginning of strng2 to be compared with strng1. If n is specified as 5 the string compare function is as follows:

```
strng1[] = "comparison";
strng2[] = "communication";
```

```
k = strncmp(strng1, strng2, 5);
```

In this case only the first five characters of strng2, which is "commu" are compared with the first five characters of strng1, which is "compa" to determine the relative magnitudes of strng1 and strng2. Since the first three characters are the same in both strings and the fourth character is different and unequal, this is sufficient to determine the relative order of the strings. In this case character p in position four of string1 is greater than m in position four of string2, which determines that string1 alphabetically follows string2. The function returns the positive value 4, to indicate that the strings differ.

If two strings differ in that one is longer than the other string as in the following example:

```
string1[] = "add";
string2[] = "addition";
```

then

```
k = strncmp(string1, string2);
```

The function returns a negative value -4, as string1 precedes string2 alphabetically and they differ in the fourth position.

The string compare functions are used to compare strings in string sorting algorithms. String comparison is also used in searching a list of strings. Searching
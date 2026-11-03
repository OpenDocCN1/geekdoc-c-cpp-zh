![](bbox=[0.07, 0.08, 0.94, 0.38])

Fig. 4.9 Illustration of string handling functions

# Other String Functions

The header file <string.h> contains many more string manipulation functions. They might be useful in certain situations.

# 4.8.5 strncpy() Function

In addition to the function strcpy that copies one string to another, we have another function strncpy that copies only the left-most n characters of the source string to the target string variable. This is a three-parameter function and is invoked as follows:

```
strncpy(s1, s2, 5);
```

This statement copies the first 5 characters of the source string s2 into the target string s1. Since the first 5 characters may not include the terminating null character, we have to place it explicitly in the 6th position of s2 as shown below:

```
s1[6] = '\0';
```

Now, the string s1 contains a proper string.

# 4.8.6 strcmp() Function

A variation of the function strcmp is the function strncmp. This function has three parameters as illustrated in the function call below:

strncmp (s1, s2, n);

this compares the left-most n characters of s1 to s2 and returns.
(a) 0 if they are equal;
(b) negative number, if s1 sub-string is less than s2; and
(c) positive number, otherwise.
# Output 2:

```
Enter string one: C programming
Enter string two: C Programming
Strings "C programming" and "C Programming" are not same.
```

# Output 3:

```
Enter string one: C Programming
Enter string two: C Programming
Strings "C Programming " and "C Programming" are not same.
```

It can be observed in Program 3 that the function strcmp takes an input of two character pointers. The first pointer points to the starting character of the first string, while the second pointer points to the starting character of the second string. It returns back an integer value that can be zero, positive, or negative.

The function strcmp starts by comparing characters stored at index 0 of both strings. If the character at index 0 of both the string is not same, then the function returns difference in ASCII values of character in string two and string one. In case the character at index 0 of both strings is same, we increment the index value by 1 and repeat the process of comparison until a mismatch is found. If the difference returned is positive, then the string one is greater than the string two; if the difference returned is negative, then the string one is less than the string two. If there is no mismatch of ASCII values, then zero is returned and the strings are said to be equal. The strings of ASCII valued to be case sensitive in Program 3; hence, character *V* is not equal to *v*.

Figure 4 shows how the three outputs have come:

![](bbox=[0.25, 0.52, 0.75, 0.735])

It can be observed in the first case of Figure 4 that the function does not find a mismatch. This causes the function to return a value zero, indicating that string one and string two are same. In the second case, the function finds a mismatch at the third character. The character stored at index *Z* of string *s_str1* is lower case *p*, while in string *s_str2*, it is upper case *P*. The function hence returns the difference in ASCII value of lower case *p* (112) and upper case *P* (80). The resultant value, as it turns out to be greater than zero, indicates that string one will come after string two in the dictionary. Similarly, in case
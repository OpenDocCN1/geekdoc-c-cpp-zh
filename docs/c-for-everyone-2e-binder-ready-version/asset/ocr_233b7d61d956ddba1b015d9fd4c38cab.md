![](bbox=[0.24, 0.08, 0.86, 0.21])

The string is declared as *const* because you are not supposed to modify a literal string. (See Special Topic 7.3 on page 320 for more information on constant pointers.)

A C string is terminated by a special character, called a *null terminator*, denoted '\0'. For example, the C string "Harry" contains six characters, namely 'H', 'a', 'r', 'r', 'y' and '\0' (See Figure 6.)

The terminator is a character that is encoded as the number zero—this is different from the character '0', the character denoting the zero digit. (Under the ASCII encoding scheme, the character denoting the zero digit is encoded as the number 48.)

Functions that operate on C strings rely on this terminator. Here is a typical example, the `strlen` function declared in the `<cstring>` header that computes the length of a character array. The function counts the number of characters until it reaches the terminator.

```
~~~c
int strlen(const char s[])
{
   int i = 0;
   while (s[i] != '\0') { i++; } // Count characters before the null terminator
   return i;
}
~~~
```

The call `strlen("Harry")` returns 5.

# ### 7.3.3 Character Arrays

A literal string such as "Harry" is a constant. You are not allowed to modify its characters. If you want to modify the characters in a string, define a character array instead. For example:

```
~~~c
char char_array[] = "Harry"; // An array of 6 characters
~~~
```

**Table 3 Character Literals**

| Literal | Description |
|---|---|
| 'y' | The character y |
| '0' | The character for the digit 0. In the ASCII code, '0' has the value 48. |
| ' ' | The space character |
| '\n' | The newline character |
| '\t' | The tab character |
| '\0' | The null terminator of a string |
| ❌ "y" | **Error:** Not a char value |
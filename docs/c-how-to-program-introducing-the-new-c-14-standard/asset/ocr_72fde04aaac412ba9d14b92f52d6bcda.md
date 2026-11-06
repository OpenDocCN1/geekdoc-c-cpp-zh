valid, and, if not, it should set `failbit` to indicate improper input. The input should be of the form

```
```cpp
{
  3 + 8i
```
```

+   C. The values can be negative or positive, and it’s possible that one of the two values is not provided, in which case the appropriate data member should be set to 0. The stream insertion operator should not be able to display the point if an input error occurred. For negative imaginary values, a minus sign should be printed rather than a plus sign.

+   D. Write a `main` function that tests input and output of user-defined class `Complex`, using the overloaded stream extraction and stream insertion operators.

+   12. 13.17 (**Printing a Table of ASCII Values**) Write a program that uses a `for` statement to print a table of ASCII values for the characters in the ASCII character set from `33` to `126`. The program should print the decimal value, octal value, hexadecimal value and character value for each character. Use the stream manipulators `dec`, `oct` and `hex` to print the integer values.

+   13. 13.18 (**String-Terminating Null Character**) Write a program to show that the `getline` and three-argument `get` `istream` member functions both end the input string with a string-
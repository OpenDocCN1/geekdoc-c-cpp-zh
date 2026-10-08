# 9.4 String Library Functions

In C there are no operators to manipulate strings because string is not a basic data type. However, C has a rich library of string manipulation functions. They are in the string.h library. This library must be included in the program in order to use these functions. The statement #include <string.h> will provide access to all of the string functions. The functions are used for the common operations of joining strings to build longer strings, comparing strings, copying strings, extracting substrings from strings, and extracting characters from strings. String functions are used to implement string operations in application software such as word processors, spreadsheets, and databases. A list of string functions are presented in Appendix B.

# 9.4.1 String Assignment

Because strings are stored as arrays, the value of one string cannot be copied to a different variable by assignment. To assign a string variable to another variable in such a way that there are two string variables with the same value, it is necessary to use the string copying function strcpy.

```
char strname1[10] = "XXABCL";
char strname2[10] = [];
```

Unless the strcpy function is used, strname1 must be copied to strname2, element-by-element by strname1 and strname2 are to have the same values.

# 9.4.2 String Copy (strcpy)

The string copy function is used to copy a string value from one variable to another string variable. There are two forms of the string copy function, one form with two arguments and another with three arguments.

First Form of the Function with Two Arguments The following code shows the use of the string copy function. This function can be used to assign the value of one string variable to another. It can also be used to replace partial strings.

```
char strng1[ ] = "Storage Technology Today";
char strng2[ ] = "Most Advanced";
```
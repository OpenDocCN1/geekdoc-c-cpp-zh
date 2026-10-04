# Chapter 9

# 505

The string Class

# string Class Functions

The string class provides a number of functions for declaring, creating, and initializing a string. In earlier versions of C++, the process of creating a new object is referred to as instantiating an object, which in this case means reinstating a string object, or creating a string, for. Table 9.2 lists the string class functions for creating and initializing an object. In class terminology, functions are formally referred to as methods, and the methods that perform the tasks of creating and initializing are called constructor methods, or constructors, for.

Table 9.2 string Class Constructors (Require the Header File string)

| Constructor | Description | Examples |
|---|---|---|n| string objectName = value | Creates and initializes a string object to a value that can be a string literal, a previously declared string object, or an expression containing string literals and string objects | string1 = "Good Morning"; string2 = str1; string3 = str1 + |
| objectName(stringValue) | Produces the same initialization as the preceding item | string1("Hot"); string1(str1 + "Dog") |
| objectName(str, n) | Creates and initializes a string object with a substring of string object starting at index n of str | string1(str2, 5) If str2 contains the string Good Morning, then str1 becomes the string Morning |
| objectName(str, n, p) | Creates and initializes a string object with a substring of string object starting at index n of str and containing p characters | string1(str2, 5,2) If str2 contains the string Good Morning, then str1 becomes the string |
| objectName(n, char) | Creates and initializes a string object with n copies of char | string1(5,'*') This makes str1 = ***** |
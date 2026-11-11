
The following table gives the basic idea of all the functions used in string.h header file.

| String functions | Its use |
| --- | --- |
| `strlen` | Returns number of characters in string |
| `strlwr` | Converts all the characters in the string into lower case characters |
| `strcat` | Adds one string at the end of another string |
| `strcpy` | Copies a string into another |
| `strcmp` | Compares two strings and returns zero if both are equal. |
| `strdup` | Duplicates a string |
| `strchr` | Finds the first occurrence of given character in a string |
| `strstr` | Finds the first occurrence of given string in another string |
| `strset` | Sets all the characters of string to given character or symbol |
| `strrev` | Reverses a string |

## Exercises

### Section A

**Multiple Choice Questions**

- 1. In `char *strcpy(char *s1, const char *s2)`
  - (a) Copies the string s2 into s1, the value of s1 is returned.
  - (b) Copies the string s1 into s2, the value of s1 is returned.
  - (c) Copies the string s2 into s1, the value of s2 is returned.
  - (d) Copies the string s1 into s2, the value of s2 is returned.
- 2. `char *strcat(char *s1, const char *s2)`
  - (a) Appends the string s1 to the end of character array s2, the value of s1 is returned.
  - (b) Appends the string s2 to the end of character array s1, the value of s1 is returned.
  - (c) Appends the string s2 to the end of character array s1, the value of s2 is returned.
  - (d) Appends the string s1 to the end of character array s2, the value of s2 is returned.
- 3. `int strcmp( const char *s1, const char *s2)`
  - (a) The function returns 0 if they are the same, a number < 0 if s1 < s2, a number > 0 if s1 > s2.
  - (b) The function returns 1 if they are the same
  - (c) The function returns <0 if they are the same
  - (d) None of the above
- 4. `strlen()` function returns
  - (a) Length of string including null character
  - (b) Length of string excluding null character
  - (c) Value of string in ASCII
  - (d) None of the above
- 5. If we have to compare first x characters of a string we will use
  - (a) strcpy
  - (b) strncpy
  - (c) strxcpy
  - (d) None of the above
- 6. In strcat function
  - (a) The null value at the end of s2 gets deleted
  - (b) The null value at the end of s1 gets deleted
  - (c) Both a and b
  - (d) None of the above
- 7. In strchr() if the char is not found in the string
  - (a) 0 is returned
  - (b) char is returned
  - (c) null is returned
  - (d) No value is returned
- 8. The library used to store all the string functions is
  - (a) string.h
  - (b) conio.h
  - (c) stdio.h
  - (d) All of the above
- 9. Strings are stored in memory as
  - (a) Pointer to address
  - (b) Array of characters
  - (c) Array of addresses
  - (d) All of the above
- 10. If we want to copy a string from one memory location to another
  - (a) strcpy()
  - (b) strncpy()
  - (c) memcpy()
  - (d) None of the above

**State True/False**

- 1. A string is an array of characters ended by a null.
- 2. The functions expect a pointer to the first character in the string.
- 3. All of the comparing functions compare full string simultaneously.
- 4. `char *strcat(char *s1, const char *s2)` statement concatenates s1 in s2.
- 5. memmove() is identical to memcpy.
- 6. strncmp compares at most n characters.
- 7. `strchr()` returns a pointer to the first occurrence of `(char)c` in `*s`.
- 8. The header `<string.h>` declares string functions.
- 9. strcpy() returns an integer value.
- 10. strcmp() function returns a char pointer.

### Section B

**Short Answer Type Questions**

- 1. Define the term string and how we handle the string in C language.
- 2. Define the working of strlen() function with suitable example.
- 3. Define the working of strcat() function with suitable example.
- 4. Define the working of strcpy() function with suitable example.
- 5. Define the working of strrev() function with suitable example.
- 6. Define the working of strlwr() function with suitable example.
- 7. Define the working of strupr() function with suitable example.
- 8. Write a program to input a string and print the string in Title Case with the help of user defined function.
- 9. Write a program to input a string and print the string in sentence case with the help of user defined function.
- 10. Write a program to input a string and print how many characters are there in that string.

### Section C

**Long Answer Type Questions**

- 1. Write a program to input a string and calculate the length of that string with the help of user defined function.
- 2. Write a program to input a string and then copy that string into another string with the help of user defined function.
- 3. Write a program to input two strings and then print the concatenated string with the help of user defined function.
- 4. Write a program to input a string and check whether the given string is palindrome or not with the help of user defined function.
- 5. Write a program to input a string and print the string in upper case with the help of user defined function.
- 6. Write a program to input a string and print the string in lowercase with the help of user defined function.
- 7. Write a program to input a text and input the string and check whether the string is available in the text or not.
- 8. Write a program to input a string and print the total number of vowels in that string.
- 9. Define the working of strncmp() function with suitable example.
- 10. Define the working of strncpy() function with suitable example.

## 13 Structure and Union

We have seen so far how to store numbers, characters, strings, and even large sets of these primitives using arrays, but what if we want to store collections of different kinds of data that are somehow related. For example, a file about an employee will probably have his/her name, age, the hours of work, salary, etc. Physically, all of that is usually stored in someone's filing cabinet. In programming, if you have lots of related information, you group it together in an organized fashion. Let us say you have a group of employees, and you want to make a database! It just would not do to have tons of loose variables hanging all over the place. Then we need to have a single data entity where we will be able to store all the related information together. But this cannot be achieved by using the arrays alone, as in the case of arrays, we can group multiple data elements that are of the same data type, and is stored in consecutive memory locations, and is individually accessed by a subscript. That is where the user defined data type *Structures* come in.

*Structure* is commonly referred to as a user-defined data type. C's *structures* allow you to store multiple variables of any type in one place (the structure). A structure can contain any of C's data types, including arrays and other structures. Each variable within a structure is named a *member* of the structure. They can hold any number of variables, and you can make arrays of structures. This flexibility makes structures ideally useful for creating databases in C. Similar to the structure there is another user defined data type called *Union* which allows the programmer to store a single storage in more than one way, i.e. a variable declared as union can store within its storage space, the data of different types, at different times. In this unit, we will be discussing the user-defined data type structures and unions.

### DEFINITION OF STRUCTURE

A structure is a collection of variables under a single name. These variables can be of different types, and each has a name which one can select it from the structure. A structure is a suitable way of grouping several pieces of related information together.

A structure can be defined as a new named type, thus extending the number of available types. It can use other structures, arrays or pointers as some of its members, though this can get complicated unless you are careful. That means we can say that structures is the collection of different data types and having a common name. A struct (short for STRUCTURE), is a collection of variables of different types. Structures are sometimes referred to as abstract data types or ADTs for short. We already know how to store a group of variables of the same type using arrays. Variables in a struct are called members or fields, and are accessed by their name. Variables in an array are called elements, and are accessed using square brackets and an index.

### DECLARATION OF STRUCTURES

To declare a structure you must start with the keyword struct followed by the structure name or structure tag and within the braces

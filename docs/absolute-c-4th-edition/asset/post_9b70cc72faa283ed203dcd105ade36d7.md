
## C-STRING VARIABLE DECLARATION

A C-string variable is the same thing as an array of characters, but it is used differently. A C-string variable is declared to be an array of characters in the usual way.

### SYNTAX

```
char Array_Name[Maximum_C-string_Size + 1];
```

### EXAMPLE

```
char myCstring[11];
```

The + 1 allows for the null character '\0', which terminates any C-string stored in the array. For example, the C-string variable myCstring in the above example can hold a C-string that is ten or fewer characters long.

Be sure you do not confuse the following initializations:

```
char shortString[] = "abc";
```

and

```
char shortString[] = {'a', 'b', 'c'};
```

They are not equivalent. The first of these two possible initializations places the null character '\0' in the array after the characters 'a', 'b', and 'c'. The second one does not put a '\0' anyplace in the array.

### INITIALIZING A C-STRING VARIABLE

A C-string variable can be initialized when it is declared, as illustrated by the following example:

```
char yourString[11] = "Do Be Do";
```

Initializing in this way automatically places the null character, '\0', in the array at the end of the C-string specified.

If you omit the number inside the square brackets, [], then the C-string variable will be given a size one character longer than the length of the C-string. For example, the following declares myString to have nine indexed variables (eight for the characters of the C-string "Do Be Do" and one for the null character '\0'):

```
char myString[] = "Do Be Do";
```

A C-string variable is an array, so it has indexed variables that can be used just like those of any other array. For example, suppose your program contains the following C-string variable declaration:

```
char ourString[5] = "Hi";
```

With ourString declared as above, your program has the following indexed variables: ourString[0], ourString[1], ourString[2], ourString[3], and ourString[4]. For example, the following will change the C-string value in ourString to a C-string of the same length consisting of all 'X' characters:

```
int index = 0;
while (ourString[index] != '\0')
{
    ourString[index] = 'X';
    index++;
}
```

When manipulating these indexed variables you should be very careful not to replace the null character '\0' with some other value. If the array loses the value '\0' it will no longer behave like a C-string variable. For example, the following will change the array happyString so that it no longer contains a C-string:

```
char happyString[7] = "DoBeDo";
happyString[6] = 'Z';
```

After the above code is executed, the array happyString will still contain the six letters in the C-string "DoBeDo", but happyString will no longer contain the null character '\0' to mark the end of the C-string. Many string-manipulating functions depend critically on the presence of '\0' to mark the end of the C-string value.

As another example, consider the above while loop that changes characters in the C-string variable ourString. That while loop changes characters until it encounters a '\0'. If the loop never encounters a '\0', then it could change a large chunk of memory to some unwanted values, which could make your program do strange things. As a safety feature, it would be wise to rewrite the above while loop as follows, so that if the null character '\0' is lost, the loop will not inadvertently change memory locations beyond the end of the array:

```
int index = 0;
while ( (ourString[index] != '\0') && (index < SIZE) )
{
    ourString[index] = 'X';
    index++;
}
```

SIZE is a defined constant equal to the declared size of the array ourString.

indexed variables for C-string variables

Do not destroy the '\0'.

### THE `<cstring>` LIBRARY

You do not need any include directive or using statement to declare and initialize C-strings. However, when processing C-strings you inevitably will use some of the predefined string functions in the library `<cstring>`. Thus, when using C-strings, you will normally give the following include directive near the beginning of the file containing your code:

```
#include <cstring>
```

The definitions in `<cstring>` are placed in the global namespace, not in the std namespace, and so no using statement is required.

### Pitfall USING = AND == WITH C-STRINGS

C-string values and C-string variables are not like values and variables of other data types, and many of the usual operations do not work for C-strings. You cannot use a C-string variable in an assignment statement using =. If you use == to test C-strings for equality, you will not get the result you expect. The reason for these problems is that C-strings and C-string variables are arrays.

Assigning a value to a C-string variable is not as simple as it is for other kinds of variables. The following is illegal:

```
char aString[10];
aString = "Hello";  // illegal!
```

Although you can use the equal sign to assign a value to a C-string variable when the variable is declared, you cannot do it anywhere else in your program. Technically, the use of the equal sign in a declaration, as in

```
char happyString[7] = "DoBeDo";
```

you obtain a safe version of `strcpy` (provided your version of C++ allows this third argument). For example:

```
char anotherString[10];
strcpy(anotherString, aStringVariable, 9);
```

With this version of `strcpy`, at most nine characters (leaving room for '\0') will be copied from the C-string variable `aStringVariable` no matter how long the string in `aStringVariable` may be.

You also cannot use the operator `==` in an expression to test whether two C-strings are the same. (Things are actually much worse than that. You can use `==` with C-strings, but it does not test for the C-strings being equal. So if you use `==` to test two C-strings for equality, you are likely to get incorrect results, but no error message!) To test whether two C-strings are the same, you can use the predefined function `strcmp`. For example:

```
if (strcmp(cString1, cString2))
    cout << "The strings are NOT the same.";
else
    cout << "The strings are the same.";
```

Note that the function `strcmp` works differently than you might guess. The comparison is true if the strings do not match. The function `strcmp` compares the characters in the C-string arguments a character at a time. If at any point the numeric encoding of the character from cString1 is less than the numeric encoding of the corresponding character from cString2, the testing stops at that point and a negative number is returned. If the character from cString1 is greater than the character from cString2, a positive number is returned. (Some implementations of `strcmp` return the difference of the character encoding, but you should not depend on that.) If the C-strings are the same, a 0 is returned. The ordering relationship used for comparing characters is called lexicographic order. The important point to note is that if both strings are in all uppercase or all lowercase, then lexicographic order is just alphabetic order.

We see that `strcmp` returns a negative value, a positive value, or zero depending on whether the C-strings compare lexicographically as lesser, greater, or equal. If you use `strcmp` as a Boolean expression in an `if` or a looping statement to test C-strings for equality, the nonzero value will be converted to true if the strings are different, and the zero will be converted to false. Be sure that you remember this inverted logic in your testing for C-string equality.

C++ compilers that are compliant with the standard have a safer version of `strcmp` that has a third argument that gives the maximum number of characters to compare.

The functions `strcpy` and `strcmp` are in the library with the header file `<cstring>`, so to use them you must insert the following near the top of the file:

```
#include <cstring>
```

The definitions of `strcpy` and `strcmp` are placed in the global namespace, not in the `std` namespace, and so no using directive is required.

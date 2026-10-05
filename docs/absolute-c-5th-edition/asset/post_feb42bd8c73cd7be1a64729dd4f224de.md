
# 37 CHAPTER 9 Strings

After the previous code is executed, the array happyString will still contain the six letters in the C-string "DoBeDo", but happyString will no longer contain the null character '\0' to mark the end of the C-string. Many string-manipulating functions depend on the presence of '\0' to mark the end of the C-value.

Another example, consider the above while loop that changes characters in the C-variable ourString. While that loop changes characters until it encounters a '\0', then it could change a large chunk of memory to unknown values, which could merge your program strings. As a safety feature, it would be wise to rewrite the while loop as follows, if the null character '\0' is lost, the loop will not inadvertently change memory locations beyond the end of the array:

```cpp
int index = 0;
while (ourString[index] != '\0') && (index < SIZE ) {
    ourString[index] = 'X';
    index++;
}
```

SIZE is a defined constant equal to the declared size of the array ourString.

## <cstring> Library

You do not need any include directive or statement to declare and initialize C-strings. However, when processing C-strings you inevitably will use some of the predefined string functions in the library <cstring>. Thus, when using C-strings, you will normally give the following include directive near the beginning of the file containing your code:

```cpp
#include <cstring>
```

The definitions in <cstring> are placed in the global namespace, not in the std namespace, and so no using statement is required.

### PITFALL: Using variables = and == with C-strings

C-string values and C-string variables are not like values and variables of other data types, and many of the usual operations do not work for C-strings. You cannot use a C-string variable in an assignment statement. If you use == to test C-strings for equality, you will not get the result you expect. The reason for these problems is that C-strings and C-string variables are arrays.

Assigning a value to a C-string is not as simple as it is for other kinds of variables. The following is illegal:

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_401_0.png)

```cpp
char aString[10];
aString = "Hello";
```

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_401_1.png)

### PITFALL: (continued)

Although you can use the equal sign to assign a value to a C-string variable when the variable is declared, you cannot do it anywhere else in your program. Technically, the use of the equal sign in a declaration, as in

```cpp
char happyString[7] = "DoBeDo";
```

is an initialization, not an assignment. If you want to assign a value to a C-string variable, you must do something else.

There are a number of different ways to assign a value to a C-string variable. The easiest way is to use the predefined function strcpy as shown here:

```cpp
strcpy(aString, "Hello");
```

This will set the value of aString to "Hello". Unfortunately, this version of the function strcpy does not check to make sure the copying exceeds the size of the string variable that is the first argument. But not all, versions of C++ have a version of strcpy (the extra 'n') that takes a third argument which gives the maximum number of characters to copy. If this third parameter is set to one less than the size of the array in the first argument you can obtain a safe version of strcpy (provided your version of C++ allows this).

```cpp
char anotherString[10]; strncpy(anotherString, aStringVariable, 9);
```

With this version of strcpy, at most nine characters (leaving room for '\0') will be copied from the C-string variable aStringVariable no matter how long the string in aStringVariable may be.

You also cannot use the operator == to test whether two C-strings are the same. (Things are actually much worse than that. You can use == with C-strings, but it does not test the C-strings being equal. If you use == to test two C-strings for equality, you are likely to get incorrect results, but no error message!) To test whether two C-strings are the same, you can use the predefined function strcmp. For example,

```cpp
if (strcmp(cString1, cString2))
cout << "The strings are not the same.";
else
cout << "The strings are the same.";
```

Note that the function works differently than you might guess. The comparison is true if the strings do not match. The function strcmp compares the characters in the C-string argument one character at a time. If at any point the numeric encoding of the character from cString1 is less than the corresponding character from cString2, the test stops at that point and a negative number is returned. If the character cString1 is greater than the character from cString2, a positive number is returned. (Some implementations of strcmp return the difference of the character encoding, but you should not depend on that.) If the C-strings are same, a 0 is returned. The ordering relationship used for comparing characters is called lexicographic order. The important point to note is if both strings are in all uppercase or lowercase, lexicographic order is just alphabetical order.

We see that strcmp returns a negative value, a positive value, or zero depending on whether the C-strings compare lexicographically as lesser, greater, or equal. If you use strcmp as a boolean expression in or a loop statement to C-strings for equality, the zero value will be converted to true if the strings are different, and the zero will be converted to false. Be sure that you inverted this logic in your testing for C-string equality.

C++ compilers that are compliant with the standard have a safer version of strcmp that has a third argument that gives the maximum number of characters to compare. The functions strcpy and strcmp are in the library with the header file <cstring>, to use them you must insert the following near the top of the file:

```cpp
#include <cstring>
```

The definitions of strcpy and strcmp are placed in the global namespace, not in the std namespace, and so no directive is required.

## Other Functions in <cstring>

Display 9.1 contains a few of the most commonly used functions from the library with the header file <cstring>. To use them, insert the following near the top of the file:

```cpp
#include <cstring>
```

The definitions in <cstring> are placed in the global namespace, not in the std namespace, and so no using statement is required.

Note that <cstring> places all definitions in the global namespace, not in the std namespace, and so no directive is required.

The function strlen is easy to understand. For example, strlen("dobedo") returns 6 because there are six characters in "dobedo".

The null character, '\0', can be used to detect the end of the C-string that is stored in the C-string variable.

Display 9.1 Some Defined C-Functions in <cstring> (part 1 of 2)

| FUNCTION | DESCRIPTION | CAUTIONS |
| --- | --- | --- |
| strcpy (Target_String_Var, Src_String) | Copies the C-string value Src_String into the C-string variable Target_String_Var. | Does not check to make sure Target_String_Var is large enough to hold the value Src_String. |
| strcpy (Target_String_Var, Src_String, Limit) | The same as the two-argument strcpy except that most characters are copied. | If Limit is chosen carefully, this is safer than the two-argument version of strcpy. Not implemented in all versions of C+. |
| strcat (Target_String_Var, Src_String) | Concatenates the C-string value Src_String onto the end of the C-string in the C-string variable Target_String_Var. | Does not check to see that Target_String_Var is large enough to hold the result of the concatenation. |
| strcat (Target_String_Var, Src_String, Limit) | The same as the two-argument strcat except that most characters are appended. | If Limit is chosen carefully, this is safer than the two-argument version of strcat. Not implemented in all versions of C+. |
| strlen (Src_String) | Returns an integer equal to the length of Src_String. (The null character, '\0', is not counted in the length.) | |

## An Array Type for Strings

A C-string variable is an array, so a C-string parameter to a function is simply an array.

## C-String Arguments and Parameters

As with any array parameter, whenever a function changes the value of a C-string, it is safest to include an additional parameter given the declared size of the C-string variable.

On the other hand, if a function only uses the value in a C-string argument but does not change that, there is no need to include another parameter to the the declared size of the C-string variable or the C-string variable that is filled.

The function is used to concatenate two C-strings to form a longer string by placing the two shorter C-strings end-to-end. The first argument must be a C-string. For example, consider the following:

```cpp
char stringVar[20] = "The rain";
strcat(stringVar, "Spain");
```

This code will change the value of stringVar to "The rainSpain".

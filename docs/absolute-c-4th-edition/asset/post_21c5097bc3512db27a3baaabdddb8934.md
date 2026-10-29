
## OTHER FUNCTIONS IN <cstring>

Display 9.1 contains a few of the most commonly used functions from the library with the header file <cstring>. To use them, insert the following near the top of the file:

```
#include <cstring>
```

Note that <cstring> places all these definitions in the global namespace, not in the std namespace, and so no using statement is required.

We have already discussed strcpy and strcmp. The function strlen is easy to understand and use. For example, strlen("dobedo") returns 6 because there are six characters in "dobedo".

The function strcat is used to concatenate two C-strings; that is, to form a longer string by placing the two shorter C-strings end-to-end. The first argument must be a C-string variable. The second argument can be anything that evaluates to a C-string value, such as a quoted string. The result is placed in the C-string variable that is the first argument. For example, consider the following:

```
char stringVar[20] = "The rain";
strcat(stringVar, " in Spain");
```

This code will change the value of stringVar to "The rain in Spain". As this example illustrates, you need to be careful to account for blanks when concatenating C-strings. If you look at the table in Display 9.1 you will see that there is a safer, three-argument version of the function strcat that is available in many, but not all, versions of C++.

### Display 9.1 Some Predefined C-String Functions in <cstring> (part 1 of 2)

| FUNCTION | DESCRIPTION | CAUTIONS |
|---|---|---|
| strcpy(Target_String_Var, Src_String) | Copies the C-string value Src_String into the C-string variable Target_String_Var. | Does not check to make sure Target_String_Var is large enough to hold the value Src_String. |
| strncpy(Target_String_Var, Src_String, Limit) | The same as the two-argument strcpy except that at most Limit characters are copied. | If Limit is chosen carefully, this is safer than the two-argument version of strcpy. Not implemented in all versions of C++. |
| strcat(Target_String_Var, Src_String) | Concatenates the C-string value Src_String onto the end of the C-string in the C-string variable Target_String_Var. | Does not check to see that Target_String_Var is large enough to hold the result of the concatenation. |
| strncat(Target_String_Var, Src_String, Limit) | The same as the two argument strcat except that at most Limit characters are appended. | If Limit is chosen carefully, this is safer than the two-argument version of strcat. Not implemented in all versions of C++. |

### Display 9.1 Some Predefined C-String Functions in <cstring> (part 2 of 2)

| FUNCTION | DESCRIPTION | CAUTIONS |
|---|---|---|
| strlen(Src_String) | Returns an integer equal to the length of Src_String. (The null character, '\0', is not counted in the length.) | |
| strcmp(String_1, String_2) | Returns 0 if String_1 and String_2 are the same. Returns a value < 0 if String_1 is less than String_2. Returns a value > 0 if String_1 is greater than String_2 (that is, returns a nonzero value if String_1 and String_2 are different). The order is lexicographic. | If String_1 equals String_2 this function returns 0, which converts to false. Note that this is the reverse of what you might expect it to return when the strings are equal. |
| strncmp(String_1, String_2, Limit) | The same as the two-argument strcmp except that at most Limit characters are compared. | If Limit is chosen carefully, this is safer than the two-argument version of strcmp. Not implemented in all versions of C++. |

## C-STRING ARGUMENTS AND PARAMETERS

A C-string variable is an array, so a C-string parameter to a function is simply an array parameter. As with any array parameter, whenever a function changes the value of a C-string parameter, it is safest to include an additional int parameter giving the declared size of the C-string variable.

On the other hand, if a function only uses the value in a C-string argument but does not change that value, then there is no need to include another parameter to give either the declared size of the C-string variable or the amount of the C-string variable array that is filled. The null character, '\0', can be used to detect the end of the C-string value that is stored in the C-string variable.

## Self-Test Exercises

- 1. Which of the following declarations are equivalent?

```
char stringVar[10] = "Hello";
char stringVar[10] = {'H', 'e', 'l', 'l', 'o', '\0'};
char stringVar[10] = {'H', 'e', 'l', 'l', 'o'};
char stringVar[6] = "Hello";
char stringVar[] = "Hello";
```

## 2. What C-string will be stored in singingString after the following code is run?

```
char singingString[20] = "DoBeDo";
strcat(singingString, " to you");
```

Assume that the code is embedded in a complete and correct program and that an include directive for <cstring> is in the program file.

## 3. What (if anything) is wrong with the following code?

```
char stringVar[] = "Hello";
strcat(stringVar, " and Good-bye.");
cout << stringVar;
```

Assume that the code is embedded in a complete program and that an include directive for <cstring> is in the program file.

## 4. Suppose the function strlen (which returns the length of its string argument) was not already defined for you. Give a function definition for strlen. Note that strlen has only one argument, which is a C-string. Do not add additional arguments; they are not needed.

## 5. What is the length (maximum) of a string that can be placed in the string variable declared by the following declaration? Explain.

```
char s[6];
```

## 6. How many characters are in each of the following character and string constants?

- a. '\n'
- b. 'n'
- c. "Mary"
- d. "M"
- e. "Mary\n"

## 7. Since character strings are just arrays of char, why does the text caution you not to confuse the following declaration and initialization?

line breaks) are skipped when C-strings are read this way. Moreover, each reading of input stops at the next space or line break. For example, consider the following code:

```
char a[80], b[80];
cout << "Enter some input:\n";
cin >> a >> b;
cout << a << b << "END OF OUTPUT\n";
```

When embedded in a complete program, this code produces a dialogue like the following:

```
Enter some input:
Do be do you!
DobeEND OF OUTPUT
```

The C-string variables a and b each receive only one word of the input: a receives the C-string value "Do" because the input character following Do is a blank; b receives "be" because the input character following be is a blank.

If you want your program to read an entire line of input, you can use the extraction operator, >>, to read the line one word at a time. This can be tedious and it still will not read the blanks in the line. There is an easier way to read an entire line of input and place the resulting C-string into a C-string variable: Just use the predefined member function getline, which is a member function of every input stream (such as cin or a file input stream). The function getline has two arguments. The first argument is a C-string variable to receive the input and the second is an integer that typically is the declared size of the C-string variable. The second argument specifies the maximum number of array elements in the C-string variable that getline will be allowed to fill with characters. For example, consider the following code:

```
char a[80];
cout << "Enter some input:\n";
cin.getline(a, 80);
cout << a << " END OF OUTPUT\n";
```

When embedded in a complete program, this code produces a dialogue like the following:

```
Enter some input:
Do be do to you!
Do be do to you!END OF OUTPUT
```

With the function cin.getline, the entire line is read. The reading ends when the line ends, even though the resulting C-string may be shorter than the maximum number of characters specified by the second argument.

When getline is executed, the reading stops after the number of characters given by the second argument has been filled in the C-string array, even if the end of the line has not been reached. For example, consider the following code:

```
char shortString[5];
cout << "Enter some input:\n";
cin.getline(shortString, 5);
cout << shortString << "END OF OUTPUT\n";
```

When embedded in a complete program, this code produces a dialogue like the following:

```
Enter some input:
dobedowap
dobeEND OF OUTPUT
```

Notice that four, not five, characters are read into the C-string variable shortString, even though the second argument is 5. This is because the null character '\0' fills one array position. Every C-string is terminated with the null character when it is stored in a C-string variable, and this always consumes one array position.

The C-string input and output techniques we illustrated for cout and cin work the same way for input and output with files. The input stream cin can be replaced by an input stream that is connected to a file. The output stream cout can be replaced by an output stream that is connected to a file. (File I/O is discussed in Chapter 12.)

## getline

The member function getline can be used to read a line of input and place the string of characters on that line into a C-string variable.

## SYNTAX

```
cin.getline(String_Var, Max_Characters + 1);
```

One line of input is read from the stream Input_Stream and the resulting C-string is placed in String_Var. If the line is more than Max_Characters long, only the first Max_Characters on the line are read. (The +1 is needed because every C-string has the null character '\0' added to the end of the C-string and thus the string stored in String_Var is one longer than the number of characters read in.)

## EXAMPLE

```
char oneLine[80];
cin.getline(oneLine, 80);
```

As you will see in Chapter 12, you can use an input stream connected to a text file in place of cin.


# CHAPTER 9 Strings

## Display 9.1 Some Predefined C-String Functions in <cstring> (part 2 of 2)

| FUNCTION | DESCRIPTION | CAUTIONS |
| --- | --- | --- |
| strcmp (String_1, String_2) | Returns 0 if String_1 and String_2 are the same. Returns a value < 0 if String_1 is less than String_2; Returns a value > 0 if String_1 is greater than String_2 (that is, returns a nonzero value if String_1 and String_2 are different). | If String_1 equals String_2, this function returns 0, which converts to false. Note that this is the reverse of what you might expect it to return when the strings are equal. |
| strncmp (String_1, String_2, Limit) | The same as the two-argument except at most Limit characters are compared. | If Limit is chosen carefully, this is safer than the two-argument version of strcmp. Not implemented in all versions of C++. |

## EXAMPLE: Command-Line Arguments

So far, have not specified any parameters for the main function. However, it is possible to specify input parameters for main. The input parameters match up with arguments given to the program when it is invoked from a command line. For example, on a UNIX machine the

```
ls /home
```

invokes the ls with the command-line argument of /home to list the contents of the /home directory. To access the command-line arguments input to a C++ program, use the following header for main:

```
int main(int argc, char *argv[])
```

The argc is an integer that specifies how many arguments are given to the program. The argv is an array of C-strings. argv[0] holds the name of the program. argv[1] holds the name of the first parameter, argv[2] holds the name of the second parameter, and so on until argv[argc-1].

For example, if the program is getPalindromes string1 and is invoked from the command line

```
getPalindromes string1
```

then inside main, argc = 3, argv[0] = "getPalindromes", argv[1] = "string1", and argv[2] = "string2".

## EXAMPLE: (continued)

If your program intends to use the contents of argv, then it should verify that arguments are actually input by ensuring argc is appropriately set. Otherwise, your program may produce incorrect results when accessing argv.

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_406_0.png)

## Self-Test Exercises

- 1. Which of the following declarations are equivalent?

```
char stringVar[10] = "Hello";
char stringVar[10] = {'H', 'e', 'l', 'l', 'o', '\0'};
char stringVar[10] = {'H', 'e', 'l', 'l', 'o', 0, 0, 0};
char stringVar[6] = "Hello"
```

- 2. C-string will be stored in singingString after the following code:
```
char singingString[20] = "DoBeDo";
strcat(singingString, " to you");
```

Assume that the code is embedded in a complete and correct program and that an include directive for <cstring> is in the program file.

- 3. What (if anything) is wrong with the following code?
```
char stringVar[] = "Hello";
strcat(stringVar, " and good-bye.");
cout << stringVar;
```

Assume that the code is embedded in a complete and correct program and that an include directive for <cstring> is in the program file.

- 4. Suppose the function strlen (which returns the length of its string argument) was not defined for you. Give a function for strlen. Note that strlen has only one argument, which is a C-string. Do not add additional arguments; they are not needed.

- 5. What is the length (maximum) of a string that can be placed in the string variable declared by the following declaration? Explain.
```
char string[6];
```

- 6. How many characters are in each of the following character and string constants?
  a. "\""
  b. "\n"
  c. "Mary"
  d. "M"
  e. "Mary\n"

## Self-Test Exercises (continued)

- 7. Since character strings are just arrays of char, why does the text caution you not to confuse the following declaration and initialization?

```
char shortString[] = "abc";
char shortString[] = {'a', 'b', 'c'};
```

- 8. Given the following declaration and initialization of the string variable, write a loop to assign 'X' to all positions of this string variable, keeping the length the same.

```
char ourString[15] = "Hi there!";
```

- 9. Consider the following declaration of a C-string variable, where SIZE is a defined constant:

The C-string variable ourString has been assigned in code not shown here. For correct C-string variables, the following loop reassigns all positions of ourString the value 'X', leaving the length the same. Assume this code fragment is embedded in an otherwise complete and correct program. Answer the questions posed by this code fragment

```
int index = 0;
while (ourString[index] != '\0') {
    ourString[index] = 'X';
    index++;
}
```

  - a. Explain how this code can decode the contents of memory beyond the end of the array.
  - b. Modify this loop to protect against inadvertently changing memory beyond the end of the array.

- 10. Write code to copy the string "Hello" into a variable using the appropriate function.

- 11. What will be the output of this code?
```cpp
char stringString[20];
strcpy(stringString, "Hello");
cout << stringString;
```

- 12. What is the problem with the following code?
```cpp
char stringString[20];
strcat(stringString, "I hope.");
cout << stringString;
```

## Input and Output

The C-input and output techniques we illustrated for cout and cin work the same way for input and output. The input stream cin can be replaced by an input stream that is connected to a file. The output stream cout can be replaced by an output stream that is connected to a file. (File I/O is discussed in Chapter 12.)

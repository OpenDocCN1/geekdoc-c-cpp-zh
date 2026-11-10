The standard library includes functions for determining the length of a string (`strlen`), copy (`strcopy`), concatenate (`strcat`) and compare (`strcmp`) two strings. You can also search for a character (`strchr`) or a string (`strstr`) in another string.

The library also includes character-oriented functions to check a character attribute or convert the case of a character.

Multiple strings can be held in a two-dimensional char array, but if the strings are known at compile time, an array of pointers would be a better choice.

A program can be run with arguments by modifying the parameter list of `main`. The variable `argc` contains the number of arguments, and the array of pointers, `argv`, contains the arguments used during invocation of the program.

# OBJECTIVE QUESTIONS

# A1.　TRUE/FALSE STATEMENTS

+   13.1　The sequence 'abcd' signifies a pointer that contains the address of 'a'.
+   13.2　The empty string "" uses no memory.
+   13.3　`stg` in the declaration `char stg[3] = "YES" ;` is not a string.
+   13.4　The string used as the first argument to `sscanf` changes every time the function reads it.
+   13.5　If a char array is not initialized on declaration, each element must be assigned individually.
+   13.6　If `p` is declared as `char *p;` and `arr` is declared as `char arr[10];`, the statement `arr = p;` is legal.
+   13.7　If `char *p = "Python";`, the statement `p[0] = 'p';` is illegal.
+   13.8　A string `s1` cannot be copied to the string `s2` by using `s2 = s1`.
+   13.9　The expression `s1 + s2` concatenates two strings to evaluate to a larger string.
+   13.10　For storing strings of unequal length, an array of char pointers is a better option than a 2D char array.
+   13.11　The command-line arguments to a C program are read by the program as strings.

# A2.　FILL IN THE BLANKS

+   13.1　A function looks for the ______ character to determine the end of a string.
+   13.2　A string can be declared as a pointer of type ______ or as an array of type ______.
+   13.3　The ______ function must not be used because it can overflow the buffer.
+   13.4　The ______ function reads data from a string and the ______ function writes data to a string.
+   13.5　For using the string-handling functions of the standard library, the file ______ must be included.
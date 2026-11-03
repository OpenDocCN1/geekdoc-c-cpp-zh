
## Summary

- A pointer is a variable that stores the memory address of another variable expressed in hexadecimal.
- The * dereference operator is used to reference the value contained in the variable to which the pointer points.
- In a pointer variable declaration, the variable name is prefixed by the * character to denote that the variable will be a pointer.
- A pointer variable can be assigned the address of another variable using the & addressof operator.
- Pointer arithmetic allows a pointer to move between consecutive memory places and is especially useful for moving between array elements.
- When an integer variable array name is assigned to a pointer, that pointer automatically stores the memory address of the first element of the array.
- Pointers can be passed as arguments to other functions.
- Passing a pointer as a function argument passes by reference, allowing that function to operate on the original value.
- Each element in an array of pointers can store the address of another variable.
- An array of pointers is especially useful for handling strings of characters.
- When a character string variable array name is assigned to a pointer, that pointer automatically stores the entire string.
- A pointer to a function must always be enclosed within parentheses when using the * dereference operator, to avoid compiler errors.
- Dereferencing a function pointer calls the function to which it points and passes any arguments specified to the pointer.

## 8 Manipulating Strings

- 110 Reading strings
- 112 Copying strings
- 114 Joining strings
- 116 Finding substrings
- 118 Validating strings
- 120 Converting strings
- 121 Summary

## Manipulating strings

![](img/d1dfb0563339ba187decb78799155b7f_111_0.png)

### Reading strings

In C programming, a string is an array of characters that has the special \0 null character in its last element. Each character, including punctuation and non-printing characters such as newline, has a unique numerical ASCII code value. This means that characters can be changed arithmetically. For example, where **char letter = 'S'** then **letter++** changes the value to 'T'. ASCII code values for lowercase letters are always 32 higher than those of uppercase letters, so the case of any character can be changed by adding or subtracting a value of 32. For example, where **char letter = 'M'** then **letter += 32** changes the value to 'm'. As C does not have a dedicated string data type, string variables must be created as character arrays, remembering to add a final element for the \0 null character to promote the array to string constant status. This means that the name of an array then acts like an implied pointer to the entire string of characters. The **sizeof** operator will return the string’s array length when the string name is supplied as its argument. A string may be assigned to an array or to a pointer of the char data type, like this:

```c
char arr[6] = { 'A', 'l', 'p', 'h', 'a' };
char *ptr = "Beta";
printf( "%s", arr );    /* Outputs "Alpha"    */
printf( "%s", ptr );    /* Outputs "Beta"     */
```

![](img/d1dfb0563339ba187decb78799155b7f_111_1.png)

You can find the standard ASCII character code table on pages 162–163.

String values can be introduced into a C program by input from the user via the **scanf()** function described on page 24. This function works well for single characters or multiple characters forming a single word, but **scanf()** has a severe limitation in that it stops reading when it encounters a space. This means that the user cannot input a sentence via **scanf()** as the string gets truncated at the space following the first word. The solution to the **scanf()** problem is provided by two alternative functions located in the **stdio.h** header file. The first of these is named **fgets()** and can be used to read input from the user. This accepts all characters, including spaces, and assigns the string to a character array specified as its first argument. Its second argument must specify the number of characters to read, and its third argument must specify where to read from, such as **stdin** to read standard input. The **fgets()** function automatically adds the \0 null character at the end of the string when the user hits the Return key – to ensure the input has string constant status. The companion to **fgets()** is the **puts()** function that will output a string specified as its argument and automatically add a newline character at the end.

![](img/d1dfb0563339ba187decb78799155b7f_111_2.png)

In C, character values must be enclosed by single quotes, and strings must be enclosed by double quotes.

![](img/d1dfb0563339ba187decb78799155b7f_111_3.png)

- 1. Begin a new program with a preprocessor instruction to include the standard input/output library functions.

```c
#include <stdio.h>
```

![](img/d1dfb0563339ba187decb78799155b7f_112_0.png)

- 2. Add a main function that declares a character array.

```c
int main()
{
    char str[51];
}
```

- 3. Next, in the main function block, request input from the user and assign it to the array variable.

```c
printf( "\nEnter up to 50 characters with spaces:\n" );
fgets( str, sizeof( str ), stdin );
```

- 4. Now, in the main function block, output the string stored in the array variable.

```c
printf( "fgets() read: " );
puts( str );
```

- 5. Repeat the process to see the scanf() limitation.

```c
printf( "\nEnter up to 50 characters with spaces:\n" );
scanf( "%s", str );
printf( "scanf() read: %s\n", str );
```

- 6. At the end of the main function block, return a zero integer value, as required by the function declaration.

```c
return 0;
```

- 7. Save the program file, then compile and execute the program to see the string results.

![](img/d1dfb0563339ba187decb78799155b7f_112_1.png)

![](img/d1dfb0563339ba187decb78799155b7f_112_2.png)

If you don't want a newline added after the output, use printf() instead of puts().

### Copying strings

![](img/d1dfb0563339ba187decb78799155b7f_113_0.png)

Ensure that the target array is of sufficient size to hold all the characters of the string being copied – including a terminating \0 null character.

The standard C libraries include a header file named string.h that contains special string-handling functions. To make these available to a program the string.h header file must be added with an #include directive at the start of the program.

One of the functions in the string.h file is strlen(), which can be used to find the length of a string supplied as its argument. The strlen() function returns an integer that is the total number of characters in the string – including space “characters”, but excluding the final \0 null character.

The string.h header file also provides two useful functions to copy strings from one array to another. The first of these is strcpy(), which requires two arguments to be specified. The first argument specifies the name of the target array to copy the string into, and the second argument specifies the name of the source array from where the string should be copied. So, its syntax looks like this:

```c
strcpy( target-array , source-array ) ;
```

All characters in the source array are copied into the target array, including the \0 null terminating character. If there are other elements after the null character these are also padded with \0. This ensures that remnants from a longer original string are removed when a shorter string is copied into an array.

The second string-copying function is the similarly named strncpy() function (with an added “n”). This is used like the strcpy() function but takes a third argument to specify how much of the string to copy. Its syntax therefore looks like this:

```c
strncpy( target-array , source-array , length ) ;
```

The string being copied will begin with the first character of the source array but will end at the position specified by the third argument – so the final \0 null character is not automatically copied. After the characters have been copied, the next element in the target array must be assigned a terminating \0 null character to promote the array to constant string status. Thus it is necessary to ensure that the target array is always one element larger than the actual number of characters being copied into it, including space “characters”, to accommodate the final \0 null character.

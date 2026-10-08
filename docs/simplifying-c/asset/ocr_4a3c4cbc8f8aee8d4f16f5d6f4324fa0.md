enter a character. Any character keyed at this point will be stored in the variable `c_choice`. A user at this point needs to enter the data carefully because pressing of space bar, Enter key, tab key, or any other nonprintable key also becomes a legitimate entry.
In Program 10, when the user enters the data, two characters are actually placed in buffer. The first character refers to the `c_choice` and the other character refers to the Enter key. Due to this, we may get a problem in reading the value of `c_choice` for the second time. To make things work, we have cleared the second character by storing its value in `c_temp`.
Most of the times, the user, rather than dealing with only a single character, deals with a set of characters called string. The next section discusses about how to input and output a string using unformatted function.

# Unformatted String I/O Functions

C language provides us with two unformatted functions `gets()` and `puts()` to input and output a string. A string in C is represented as a set of characters that is always terminated with a null character (\0). The syntax of the unformatted string I/O function is as follows:

```
gets(identifier name); and puts(identifier name);
```

Program 11 illustrates the use of unformatted string I/O functions:

# Program 11

```
/** Program to illustrate how to read and display strings **/
#include<stdio.h>
/** Beginning of main function **/
main()
{
/** Declare character array **/
char s_city[50];

/** Read data in array **/
printf("\nEnter the name of city: ");
gets(s_city);

/** Print data from array **/
printf("\nThe name of the city is: ");
puts(s_city);
printf("\n");
return;
}
/** End of function main **/
```

**Output:**

Enter the name of city: Ahmedabad
The name of the city is: Ahmedabad

In Program 11, the `gets` function takes the name of the character array as a parameter and stores the data in it. The data is read from the standard input stream till the user presses the Enter key. The function then discards the newline character and stores the
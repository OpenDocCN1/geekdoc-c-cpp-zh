# Reading a Line of Text

In many text processing applications, we need to read in an entire line of text from the terminal. It is not possible to use scanf function to read a line containing more than one word. This is because the scanf terminates reading as soon as a space is encountered in input.

We have discussed in Chapter 5 as to how to read a single character from the terminal, using the function getchar(). We can use this function repeatedly to read successive single characters from the input and place them into a character array. Thus, an entire line of text can be read and stored in an array. The reading is terminated when the newline character ('\n') is entered and the null character is then inserted at the end of the string.

# Example 9.2

Write a program to read a line of text containing a series of words from the terminal.

The program shown in Fig. 9.2 can read a line of text (upto a maximum of 80 characters) into the string line. Every time a character is read, it is assigned to its location in the string line and then tested for newline character. When the newline character is read (signalling the end of line), the reading loop is terminated and the newline character is replaced by the null character to indicate the end of character string.

```
Program
/*
* PROGRAM TO READ A LINE OF TEXT FROM TERMINAL
*/
#include <stdio.h>
main()
{
 char line [81], character;
 int c;
 c = 0;
 printf("Enter text. Press <Return> at end\n");
 do
 {
 character = getchar();
 line[c] = character;
 c++;
 }
 while(character != '\n');
 c = c - 1;
 line[c] = '\0';
 printf("\n%s\n", line);
}
```

Output
Enter text. Press <Return> at end
Programming in C is interesting.
Programming in C is interesting.
Enter text. Press <Return> at end
National Computing Centre, United Kingdom.
National Computing Centre, United Kingdom.

Fig. 9.2 Program to read a line of text from terminal
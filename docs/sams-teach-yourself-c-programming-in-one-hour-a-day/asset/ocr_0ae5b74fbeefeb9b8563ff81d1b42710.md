10. Using a defined constant is common in looping; you can see examples similar to this code fragment in lessons throughout the book. The problem with this fragment is simple. The semicolon doesn't belong at the end of the for statement. This is a common bug.

# Answers for Lesson 7

# Quiz

+   1. There are two differences between puts() and printf():
   printf() can print variable parameters.
   puts() automatically adds a newline character to the end of the string it prints.
2. You should include the stdio.h header file using printf().
3. a. \ prints a backslash.
   b. \b prints a backspace.
   c. \n prints a newline.
   d. \t prints a tab.
   e. \a for "alert" sounds the beep.
4. a. %s for a character string
   b. %d for a signed decimal integer
   c. %f for a decimal floating-point number
5. a. b prints the literal character b.
   b. \ prints a backspace character.
   c. \ looks at the next character to determine an escape character (see Table 7.1).
   d. \ prints a single backslash.

# Exercises

+   1. puts() automatically adds the newline; printf() does not. The code is as follows:
   printf("\n");
   puts(" ");
2. The code is as follows:
   char c1, c2;
   int d1;
   scanf("%c %u %c", &c1, &d1, &c2);
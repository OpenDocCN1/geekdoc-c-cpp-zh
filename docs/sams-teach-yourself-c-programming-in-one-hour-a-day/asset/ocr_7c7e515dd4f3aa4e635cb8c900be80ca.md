# Displaying Strings and Characters

# LISTING 10.4 put:c: Using the puts() Function to Display Text Onscreen

```
1: /* demonstrates displaying strings with puts(). */
3: #include <stdio.h>
4: 
5: char *message1 = "C";
6: char *message2 = "is the";
7: char *message3 = "best";
8: char *message4 = "programming";
9: char *message5 = "language!";
10: 
11: int main( void )
12: {
13: puts(message1);
14: puts(message2);
15: puts(message3);
16: puts(message4);
17: puts(message5);
18: 
19: return 0;
20: }
```

# Output

c
is is the
best
programming
language!!

# Analysis

This is a fairly simple listing to follow. Because puts() is a standard output function, the stdio.h header file needs to be included, as done on line 3. Lines 5 through 9 declare and initialize five different variables. Each of these variables is a character pointer, or string variable. Lines 13 through 17 use the puts() function to print each string.

# The printf() Function

You can also display strings using the printf() library function. Recall from Lesson 7 that printf() uses a format string and various converters to shape its output. To display a string, use the conversion specifier %s.

When printf() encounters a %s in its format string, the function matches the %s with the corresponding argument in its argument list. For a string, this argument must be a
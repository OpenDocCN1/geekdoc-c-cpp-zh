# LESSON 14 Working with the Screen, Printer, and Keyboard

```
39: puts("Enter your first and last names separated by a space.");
40: scanf("%[^ ]%s", buf1, buf2);
41: printf("\nYour first name is %s\n", buf1);
42: printf("Your last name is %s\n", buf2);
43: puts("Note how [^ ] is in the scanf() format string, by excluding");
44: puts("the space character, caused the input to be split.");
45:
46: return 0;
47: }
```

# Output ▼

Enter an integer and a floating point number.
123 45.67890

You entered 123 and 45.67890.
The scanf() format string used the 1 modifier to store\your input in a type long and a double.

Enter a 5 digit integer (for example, 54321).
54321

You entered 54 and 321.
Note how the field width specifier in the scanf() format
string split your input into two values.

Enter your first and last names separated by a space.
Ruth Alber

Your first name is Ruth
Your last name is Alber
Note how [^ ] in the scanf() format string, excluding
t space character, caused the input to be split.

# Analysis ▼

This listing starts by defining several variables on lines 7 through 13 for data input.
The program walks through the steps of entering various types of data. Lines
17 through 21 have you enter and print integers and a double. Line 23 calls the
flush() function to clear any unwanted characters from the standard input stream.
Lines 27 and 28 get the value, a five-character integer. Because there are width
specifiers, the five-digit integer is split into two integers—one that is two characters
 one that is three characters. Line 34 calls flush() to clear the keyboard again.
The final example, in lines 36 through 44, use the exclude character. Line 40 uses
"%[^ ]", which tells scanf() to get a string to stop at any spaces. This effectively
splits the input.
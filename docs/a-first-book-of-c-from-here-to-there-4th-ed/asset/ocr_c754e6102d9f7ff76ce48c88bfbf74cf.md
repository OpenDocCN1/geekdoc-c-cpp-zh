# Point of Information

# The string and char Data Types

A string can consist of zero, one, or more characters. When the string has no characters, it's said to be an empty string with a length of 0. A string with a single character, such as "a", is a string of length 1 and is stored differently from a char data type, such as 'a'. However, for many practical purposes, a string of length 1 and a char respond in the same manner; for example, both cout >> "\n" and cout >> '\n' produce a new line onscreen. It's important to understand that they're different data types. For example, both these declarations

```
string s1 = 'a';  // INVALID INITIALIZATION
char key = "\n"; // INVALID INITIALIZATION
```

produce a compiler error because they attempt to initialize one data type with literal values of another type.

![](bbox=[0.22, 0.58, 0.85, 0.75])

# Figure 14.4 Typed characters are first stored in a buffer

The cin input stream in Program 14.3 accepts the number entered but leaves the '\n' in the buffer. The next input statement, which is a call to getline(), picks up the code for the Enter key as the next character and terminates any further input. Following is a sample run of Program 14.3:

```
Enter a number: 26
The number entered is 26
Enter text:
The text entered is
```

In this output, no text is accepted in response to the prompt Enter text:. No text is accepted because after the program accepts the number 26, the code for the Enter key, which is a newline escape sequence, remains in the buffer and is picked up and interpreted by getline() as the end of its input. This result occurs whether an integer (as in Program 14.3), a string, or any
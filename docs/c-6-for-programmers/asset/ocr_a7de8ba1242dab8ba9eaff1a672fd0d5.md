```
10  Console.WriteLine("Welcome\nto\nC#\nProgramming!");
11 } // end Main
12 } // end class Welcome3
```

![](bbox=[0.2, 0.25, 0.88, 0.37])

Fig. 3.11 | Displaying multiple lines with a single statement. (Part 2 of 2.)

Most of the app is identical to the apps of Fig. 3.1 and Fig. 3.10, so we discuss only the changes here. Line 2

```
// Displaying multiple lines with a single statement.
```

states the purpose of this app. Line 5 begins the Welcome3 class declaration.

```
Console.WriteLine("Welcome\nto\nC#\nProgramming!");
```

displays four separate lines of text in the console window. Normally, the characters in a string are displayed exactly as they appear in the double quotes. Note, however, that the two characters \ and n (repeated three times in the statement) do not appear on the screen. The backslash (\) is called an escape character. It indicates to C# that a "special character" is in the string. When a backslash appears in a string of characters, C# combines the next character with the backslash to form an escape sequence.

| Escape sequence | Description |
|---|---|
| \n | Newline. Positions the screen cursor at the beginning of the next line. |
| \t | Horizontal tab. Moves the screen cursor to the next tab stop. |
| \" | Double quote. Used to place a double-quote character (") in a string—e.g., Console.Write("\"in quotes\""); displays "in quotes". |

Fig. 3.12 | Common escape sequences. (Part 1 of 2.)
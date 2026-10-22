| Sequence | Meaning |
|---|---|
| \" | Double quote ("). |
| \? | Question mark (?). |
| \ooo | Octal value. (o represents an octal digit.) |
| \xhh | Hexadecimal value. (h represents a hexadecimal digit.) |

Escape sequences must be enclosed in single quotes when assigned to a character variable. For example, you could make the statement

```
char nerf = '\n';
```

and then print the variable nerf to advance the printer or screen one line.

Now take a closer look at what each escape sequence does. The alert character (\a), added by C90, produces an audible or visible alert. The nature of the alert depends on the hardware, with the beep being the most common. (With some systems, the alert character has no effect.) The C standard states that the alert character shall not change the active position. By active position, the standard means the location on the display device (screen, teletype, printer, and so on) at which the next character would otherwise appear. In short, the active position is a generalization of the screen cursor with which you are probably accustomed. Using the alert character in a program displayed on a screen should produce a beep without moving the screen cursor.

Next, the \b, \f, \n, \r, \t, and \v escape sequences are common output device control characters. They are best described in terms of how they affect the active position. A backspace (\b) moves the active position back one space on the current line. A form feed character (\f) advances the active position to the start of the next page. A newline character (\n) sets the active position to the beginning of the next line. A carriage return (\r) moves the active position to the beginning of the current line. A horizontal tab character (\t) moves the active position to the next horizontal tab stop (typically, these are found at character positions 1, 9, 17, 25, and so on). A vertical tab (\v) moves the active position to the next vertical tab position.

These escape sequence characters do not necessarily work with all display devices. For example, the form feed and vertical tab characters produce odd symbols on a PC screen instead of any cursor movement, but they work as described if sent to a printer instead of to the screen.

The next three escape sequences (\\, \', and \") enable you to use \, ', and " as character constants. (Because these symbols are used to define character constants as part of a printf() command, the situation could get confusing if you use them literally.) Suppose you want to print the following line:

```
Gramps sez, "a \ is a backslash."
```

Then use this code:

```
printf("Gramps sez, \"a \\ is a backslash.\"\n");
```
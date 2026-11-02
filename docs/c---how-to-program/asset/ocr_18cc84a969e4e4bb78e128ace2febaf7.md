```
int main(void)
{
    printf("%+09d\n", 452);
    printf("%09d\n", 452);
}
```

```
+00000452
000000452
```

Fig. 9.15 | Using the 0 (zero) flag. (Part 2 of 2.)

# 9.10 Printing Literals and Escape Sequences

As you've seen throughout the book, literal characters included in the format control string are simply output by printf. However, there are several "problem" characters, such as the quotation mark (") that delimits the format control string itself. Various control characters, such as newline and tab, must be represented by escape sequences. An escape sequence is represented by a backslash (\), followed by a particular escape character. Figure 9.16 lists the escape sequences and the actions they cause.

| Escape sequence | Description |
|---|---|
| \' (single quote) | Output the single quote (') character. |
| \" (double quote) | Output the double quote (") character. |
| \? (question mark) | Output the question mark (?) character. |
| \\ (backslash) | Output the backslash (\) character. |
| \a (alert or bell) | Cause an audible (bell) or visual alert (typically, flashing the window in which the program is running). |
| \b (backspace) | Move the cursor back one position on the current line. |
| \f (new page or form feed) | Move the cursor to the start of the next logical page. |
| \n (newline) | Move the cursor to the beginning of the next line. |
| \r (carriage return) | Move the cursor to the beginning of the current line. |
| \t (horizontal tab) | Move the cursor to the next horizontal tab position. |
| \v (vertical tab) | Move the cursor to the next vertical tab position. |

Fig. 9.16 | Escape sequences.

# 9.11 Reading Formatted Input with scanf

Precise input formatting can be accomplished with scanf. Every scanf statement contains a format control string that describes the format of the data to be input. The format control string consists of conversion specifiers and literal characters. Function scanf has the following input formatting capabilities:

+   1. Inputting all types of data.
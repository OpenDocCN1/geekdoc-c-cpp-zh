In other words, the Return (or Enter) key on your keyboard cannot be part of the string. That is, in programming code, a string *cannot* be broken into more than one line by using the return (Enter) key on your keyboard.

Recall that the newline character is **\n**, which causes the insertion point to move to the beginning of the next line. There are many escape sequences in C++, which allow you to control the output. Table 2-4 lists some of the commonly used escape sequences.

**TABLE 2-4  Commonly Used Escape Sequences**

| Escape Sequence | Description |
|---|---|
| `\n` | Newline — Cursor moves to the beginning of the next line |
| `\t` | Tab — Cursor moves to the next tab stop |
| `\b` | Backspace — Cursor moves one space to the left |
| `\r` | Return — Cursor moves to the beginning of the current line (not the next line) |
| `\\` | Backslash — Backslash is printed |
| `\'` | Single quotation — Single quotation mark is printed |
| `\"` | Double quotation — Double quotation mark is printed |

The following example shows the effect of some of these escape sequences.

# EXAMPLE 2-26

The output of the statement:

```
cout << "The newline escape sequence is \\n" << endl;
```

is:

```
The newline escape sequence is \n
```

The output of the statement:

```
cout << "The tab character is represented as '\\t'" << endl;
```

is

```
The tab character is represented as '\t'
```

Note that the single quote can also be printed without using the escape sequence. Therefore, the preceding statement is equivalent to the following output statement:

```
cout << "The tab character is represented as '\\t'" << endl;
```
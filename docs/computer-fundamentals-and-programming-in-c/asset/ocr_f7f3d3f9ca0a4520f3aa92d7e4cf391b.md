unpredictable. To avoid this type of problem, it is usually a good idea not to include constant text in format strings when using `scanf()`.

When reading in integers or floats, the `scanf()` function skips leading white space. This means that all spaces, tabs, and new line characters will be ignored, and `scanf()` will keep reading input until it reaches a number. When reading in a character, `scanf()` will read exactly one character, which can be any valid ASCII character or other valid character for the system. If the user wants to skip a space before a character, the space has to be explicitly included in the character string. For example, consider the following code, assuming that `a`, `b`, and `c` are integers and `x` is a character.

```
```c
scanf("%d%d%d%c", &a, &b, &c, &x);
```
```

Assume that the user wants `a`, `b`, `c`, and `x` to be 1, 2, 3, and Z. The user would have to type

```
```text
1 2 3z
```
```

If, instead, the user types

```
```text
1 2 3 Z
```
```

then the value of `x` will be a space because `z` has been typed with a space preceding it.

If the user wants to be able to enter the line this way, the `scanf()` needs to be coded as follows:

```
```c
scanf("%d%d%d %c", &a, &b, &c, &x);
```
```

Using spaces between integer field specifications is optional. For example, while reading integers `x`, `y`, and `z`

```
```c
scanf("%d%d%d", &x, &y, &z);
```
```

is equivalent to

```
```c
scanf("%d %d %d", &x, &y, &z);
```
```

Normally, when reading a numeric value, `scanf()` reads until it sees trailing white space. The rule is that `scanf()` processes the format string from left to right and each time it reaches a specifier it tries to interpret what has been typed as a value. If multiple values are input, these are assumed to be separated by white space, i.e., spaces, new line, or tabs. This means, the user can type

```
```text
3 4 5
```
```

or

```
```text
3
4
5
```
```

and it does not matter how many spaces are included between items. For example,

```
```c
scanf("%d %d", &i, &j);
```
```

will read in two integer values into `i` and `j`. The integer values can be typed on the same line or on different lines as long as there is at least one white space character between them. The only exception to this rule is the `%c` specifier that always reads in the next character typed no matter what it is.

If a width modifier is used, it specifies the maximum number of characters to be read.

Then `scanf()` will read either as many characters as specified by the width modifier or until it sees white space, whichever happens first. In this case, its effect is to limit the number of characters accepted to the width. For example,

```
```c
scanf("%10d", &i);
```
```

would use at most the first ten digits typed as the new value for `i`. There are two other reasons that can cause `scanf()` to stop. One is if an end-of-file character is encountered. When reading from an actual disk file, there is automatically an end-of-file character at the end of the file. When reading from a keyboard, the user can simulate one by pressing a specific character sequence. On UNIX machines, the user can enter an end-of-file character by pressing `Ctrl-D`.

The other reason that may cause `scanf()` to stop is when it encounters an invalid input. For instance, if `scanf()` is expecting to read a numeric value and it comes across a non-numeric character, this is an error.

The following are the reasons because of which `scanf()` will stop reading a value for a variable.

+   * A white space character is found after a digit in a numeric sequence.
+   * The maximum number of characters has been processed.
+   * An end-of-file character is reached.
+   * An error is detected.

The `scanf()` function returns the number of variables successfully read in. For example, consider the following program.

# EXAMPLE

```
```c
21. #include <stdio.h>
    int main(void)
    {
      int a, b, c;
      int num;
      num = scanf("%d %d %d", &a, &b, &c);
      printf("I have read %d values.\n", num);
      return 0;
    }
```
```

When run, the user must type `10 20 30` for the program to output

```
```text
I have read 3 values.
```
```

If the user types `10 20 hello`, the program will output

```
```text
I have read 2 values.
```
```

If the user types `hello 10 20 30`, the program will output

```
```text
I have read 0 values.
```
```

When reading standard input from the keyboard, the input is buffered. In other words, the program does not see the text
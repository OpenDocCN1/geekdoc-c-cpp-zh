You can list more than one variable in a single `cin` statement, as illustrated by the following:

```cpp
cout << "Enter the number of dragons\n"
     << "followed by the number of trolls.\n";
cin >> dragons >> trolls;
```

If you prefer, the above `cin` statement can be written on two lines, as follows:

```cpp
cin >> dragons
    >> trolls;
```

Notice that, as with the `cout` statement, there is just one semicolon for each occurrence of `cin`.

When a program reaches a `cin` statement, it waits for input to be entered from the keyboard. It sets the first variable equal to the first value typed at the keyboard, the second variable equal to the second value typed, and so forth. However, the program does not read the input until the user presses the Return key. This allows the user to backspace and correct mistakes when entering a line of input.

Numbers in the input must be separated by one or more spaces or by a line break. When you use `cin` statements, the computer will skip over any number of blanks or line breaks until it finds the next input value. Thus, it does not matter whether input numbers are separated by one space or several spaces or even a line break.

You can read in integers, floating-point numbers, or characters using `cin`. Later in this book we will discuss the reading of other kinds of data using `cin`.

# CIN STATEMENTS

A `cin` statement sets variables equal to values typed in at the keyboard.

# SYNTAX

```
cin >> variable_1 >> variable_2 >> ...;
```

# EXAMPLES

```
cin >> number >> size;
cin >> timeLeft
    >> pointsNeeded;
```
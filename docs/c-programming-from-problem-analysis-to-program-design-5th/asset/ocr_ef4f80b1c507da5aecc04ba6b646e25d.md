In C++, output on the standard output device is accomplished via the use of `cout` and the operator `<<`. The general syntax of `cout` together with `<<` is:

```
cout << expression or manipulator << expression or manipulator...;
```

This is called an **output statement**. In C++, `<<` is called the **stream insertion operator**. Generating output with `cout` follows two rules:

+   1. The expression is evaluated, and its value is printed at the current insertion point on the output device.
+   2. A manipulator is used to format the output. The simplest manipulator is `endl` (the last character is the letter el), which causes the insertion point to move to the beginning of the next line.

> **NOTE**  On the screen, the insertion point is where the cursor is.

The next example illustrates how an output statement works. In an output statement, a string or an expression involving only one variable or a single value evaluates to itself.

> **NOTE**  When an output statement outputs `char` values, it outputs only the character without the single quotes (unless the single quotes are part of the output statement).

For example, suppose `ch` is a `char` variable and `ch = 'A';`. The statement:

```
cout << ch;

or:

cout << 'A';

outputs:

A
```

Similarly, when an output statement outputs the value of a string, it outputs only the string without the double quotes (unless you include the quotes as part of the output).

# EXAMPLE 2-21

Consider the following statements. The output is shown to the right of each statement.

| Statement | Output |
|---|---|
| `cout << 29 / 4 << endl;` | `7` |
| `cout << "Hello there." << endl;` | `Hello there.` |
| `cout << 12 << endl;` | `12` |
| `cout << "4 + 7" << endl;` | `4 + 7` |
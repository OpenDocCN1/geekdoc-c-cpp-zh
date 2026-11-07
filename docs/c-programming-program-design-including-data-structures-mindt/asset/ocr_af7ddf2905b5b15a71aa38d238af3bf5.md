```
8                       Line 12
3 + 5 **                Lines 13 and 14
20                      Line 16
a                       Line 17
65                      Line 18
78                      Line 19
```

For the most part, the output is straightforward. Look at the output of the statements in Lines 12, 13, 14, and 15. The statement in Line 12 outputs the result of 3 + 5, which is 8, and moves the insertion point to the beginning of the next line. The statement in Line 13 outputs the string 3 + 5. Note that the statement in Line 13 consists only of the string 3 + 5. Therefore, after printing 3 + 5, the insertion point stays positioned after 5; it does not move to the beginning of the next line. The next output of the statement in Line 14 outputs a space and ** at the insertion point, which was positioned after 5.

The output statement in Line 15 contains only the manipulator endl, which moves the insertion point to the beginning of the next line. Therefore, when the statement in Line 16 executes, the output starts at the beginning of the line. Note that in this output, the column “Output of Statement at” does not contain Line 15. This is due to the fact that the statement in Line 15 does not produce any printable output. It simply moves the insertion point to the beginning of the next line. Next, the statement in Line 16 outputs the value of 2 + 3 * 6, which is 20. The manipulator endl then moves the insertion point to the beginning of the next line.

> > **NOTE**  Outputting or accessing the value of a variable in an expression does not destroy or modify the contents of the variable.

Let us now take a close look at the newline character, '\n'. Consider the following C++ statements:

```
cout << "Hello there.";
cout << "My name is James.";
```

If these statements are executed in sequence, the output is:

```
Hello there.My name is James.
```

Now consider the following C++ statements:

```
cout << "Hello there.\n";
cout << "My name is James.";
```

The output of these C++ statements is:

```
Hello there.
My name is James.
```
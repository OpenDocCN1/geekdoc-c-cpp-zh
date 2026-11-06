# Indentation and Lines

There are no braces for the indication of blocks of code for class definition and function in Python. Likewise, flow control is not included. If you want to denote such blocks of code, you have to make use of line indentation. You can adjust it for spaces, but make sure to indent all statements with a block, too. To help you understand this further, consider the following sample codes:

```
if True:
    print “ Correct ”
else:
    print “ Incorrect ”
```

```
if True
    print “ Input ”
    print “ Correct ”
else:
    print “ Input ”
    print “ False
```

Running the first given example generates an output. Running the second one, however, results in an error. Why did this happen? Well, you have to keep in mind that in Python, blocks are formed by indenting continuous lines with the same amount of space.

Indentation is simply a way to group statements. Programmers use it in place of curly braces of blocks of code. Tabs and spaces are supported, but standard indentation requires standard codes to have similar amounts of spaces. In general, four spaces are used. Take a look at the following example:

```
w = 1
```
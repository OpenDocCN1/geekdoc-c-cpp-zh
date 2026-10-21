# # Data, Variables, and Calculations

If you compile and execute this example, it produces the following output:

> "We'll make our escapes in sequence", he said.
> 
> The program's over, it's time take make a beep beep.

# ## How It Works

The first line in main() defines the variable newline and initializes it with a character defined by the escape sequence for a new line. You can then use newline instead of endl from the standard library.

# ## Calculating in C++

This is where you actually start doing something with the data that you enter. You know how to carry out simple input and output; now you are beginning the bit in the middle, the "processing" part of a C++ program. Almost all of the computational aspects of C++ are fairly intuitive, so you should slice through this like a hot knife through butter.

# ## The Assignment Statement

You have already seen examples of the assignment statement. A typical assignment statement looks like this:

```
whole = part1 + part2 + part3;
```

The assignment statement enables you to calculate the value of an expression which appears on the right hand side of the equals sign, in this case the sum of part1, part2, and part3, and store the result in the variable specified on the left hand side, in this case the variable with the name whole. In this statement, the whole is exactly the sum of its parts and no more.

Note how the statement, as always, ends with a semicolon.

You can also write repeated assignments such as,

```
a = b = 2;
```

This is equivalent to assigning the value 2 to b and then assigning the value of b to a, so both variables will end up storing the value 2.
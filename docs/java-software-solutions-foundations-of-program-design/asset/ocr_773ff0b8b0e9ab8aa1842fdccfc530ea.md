Note that in the temperature conversion program, the operands to the division operation are floating point literals to ensure that the fractional part of the number is kept. The precedence rules dictate that the multiplication happens before the addition in the final conversion computation.

The TempConverter program is not very useful because it converts only one data value that we included in the program as a constant (24 degrees Celsius). Every time the program is run it produces the same result. A far more useful version of the program would obtain the value to be converted from the user each time the program is executed. Interactive programs that read user input are discussed later in this chapter.

# Increment and Decrement Operators

There are two other useful arithmetic operators. The increment operator (++) adds 1 to any integer or floating point value. The two plus signs that make up the operator cannot be separated by white space. The decrement operator (--) is similar except that it subtracts 1 from the value. They are both unary operators because they operate on only one operand. The following statement causes the value of count to be incremented:

```
count++;
```

The result is stored back into the variable count. Therefore it is functionally equivalent to the following statement, which we discussed in the previous section:

```
count = count + 1;
```

The increment and decrement operators can be applied after the variable (such as count++ or count--), creating what is called the postfix form of the operator. They can also be applied before the variable (such as ++count or --count), in what is called the prefix form. When used alone in a statement, the prefix and postfix forms are functionally equivalent. That is, it doesn’t matter if you write

```
count++;
```

or

```
++count;
```

However, when such a form is written as a statement by itself, it is usually written in its postfix form.

When the increment or decrement operator is used in a larger expression, it can yield different results depending on the form used. For example, if the variable
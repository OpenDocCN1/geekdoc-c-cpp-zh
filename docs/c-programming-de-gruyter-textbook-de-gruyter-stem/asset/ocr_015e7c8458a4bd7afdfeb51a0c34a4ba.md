# 48 — 2 Elementary C++ Programming

It outputs the character string "a+b=$\ and the result of $a+b$ successively to the screen.
The most general keyboard input is to use the input operator on stream-type object cin. The format is:

```
cin>>expression >>expression...
```

In an input statement, one can write several input contiguously, each followed by an expression that stores the input variable. For example:

```
int a,b;
cin>>a>>b;
```

To input two int-type numbers from the keyboard, we can use space to separate the two numbers. If one enters:

5 6

Then the value of variable a is 5 and the value of variable b is 6.

# 2.3.3 Simple I/O Format Control

When using cin and cout for input and output, computers can process any type of data according to the default format automatically. But this is not enough. We often need special formats. There are many ways to set a format, and we will detail them in Chapter 11. In this section we only include the simplest format control.

A C++ I/O-stream library provides some operators that can be directly embedded into the input/output statements to achieve I/O format control. To use these operators, we should first include an iomanip header file at the beginning of the source program. The commonly used I/O-stream library operators are listed in Table 2.6.

For example, if you want to output a floating number 3.1415 to the screen and jump to a new line, you can set the field width to five characters and keep significant digits the decimal point. The output would be:

```
cout<<setw(5)<<setprecision(3)<<3.1415<<endl;
```

Tab. 2.6: Commonly Used I/O-stream Library Operators.

| Operator Name | Meaning |
|---|---|
| Dec | Use decimal system to represent data |
| Hex | Use hexadecimal system to represent data |
| Oct | Use octal system to represent data |
| W | Extract blank characters |
| endl | Insert line break and flush the stream |
| Ends | Insert the null character |
| setprecision (int) | Set decimal digits of a floating number (include decimal point) |
| setw (int) | Set field width |
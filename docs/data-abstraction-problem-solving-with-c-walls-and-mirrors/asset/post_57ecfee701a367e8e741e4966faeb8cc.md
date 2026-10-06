
Two more operators, ++ and --, provide convenient incrementing and decrementing operations:

The operators ++ and -- are useful for incrementing and decrementing a variable

a++ means a += 1, which means a = a + 1.

Similarly,

a-- means a -= 1, which means a = a - 1.

The operators ++ and -- can either follow their operands, as you just, or precede them. Although ++a, for instance, has the same effect as a++, the results differ when the operators are combined with assignment. For example:

b = ++a means b = a + 1; b = a

Here, the ++ operator acts on a before assigning a's new value to b. In contrast,

b = a++ means b = a + 1

The assignment operator assigns a's value to b before the ++ operator acts on a. That is, the ++ operator acts on a after the assignment. The ++ and -- are often used within loops and array indices, as you will see later in this appendix. When we use these operators with arithmetic variables, we write the operator after the variable.

In addition to the operators described here, C++ provides several other operators. A summary of all C++ operators and their precedes is inside the cover of this book.

## A.2 Input and Output Using iostream

A typical C++ program reads its input from keyboard and writes its output to a display. Input and output consist of characters, which are simply sequences of characters that either come from or go to an input or output (i/o) device.

The data type of an input stream is istream, and the data type of an output stream is ostream. The iostream library provides these data types and three default stream variables: cin for the standard input stream, cout for the standard output, and cerr for the standard error stream, which is also an output stream. Your program gains access to the iostream library by including the iostream header file. This section provides a brief introduction to simple input and output.

### A.2.1 Input

C++ provides the input operator >> to read integers, floating-point numbers, and characters into variables data types are any of the fundamental data types. The input operator >> reads from an input as its left operand and the variable that will contain the value as its right operand.

Thus,

```
cin >> x;
```

reads a value for x from the standard input stream. The >> operator is left-associative. Thus,

```
cin >> x >> y
```

means

```
(cin >> x) >> y
```

That is, by these expressions read characters for x from the input stream and then read subsequent characters for y.

The input operator >> skips whitespace, such as blanks, tabs, and new-line characters, that might occur values in the input data line. For example, after the program segment

```
int ia = 0;
int ib = 0;
double da = 0;
double db = 0;
cin >> ia >> da >> ib;
cin >> db;
```

reads the data line

```
21 -3.45 -6 475.1e-2 <eol>
```

the variable ia contains 21, da contains -3.45, ib contains -6, and db contains 475.1. A subsequent attempt to read from cin will look at the end of the line (<eol>) and read from the next data line, if one exists. An error occurs if no data exists for a corresponding variable processed by >> or if the variable's data type does not match the type of data available. For example, the previous program segment reads the data line

```
-1.23 456.1e-2 -7 8 <eol>
```

the variable ia contains -1, da contains 0.23, ib contains 456, and db contains 0.001. The rest of the data line is left for a subsequent read, if any example, if the segment attempts to read a data line that begins with .21, the read would terminate ia is int and -21 is not.

an expression like cin >> x has a value after the read operation takes place. If the operation is successful, this is true; otherwise it is false. You can examine this value by using the selection and iteration statements that described later in this appendix.

You also use the >> operator to read individual characters from the input stream into variables. Any whitespace is skipped. For example, after the program segment

```
char ch1 = ' ';
char ch2 = ' ';
char ch3 = ' ';
cin >> ch1 >> ch2 >> ch3;
```

reads the data line

```
xyz
```

ch1 contains 'x', ch2 contains 'y', and ch3 contains 'z'.

You can read whitespace when reading individual characters into character variables by using the C++ method get. Either of the statements

```
cin.get(ch1);
```

or

```
ch1 = cin.get();
```

reads the next character, even if it is a blank, a tab, or a new-line character, from the input stream into the char variable ch1.

Section A.7, later in this appendix, describes how to read character strings.

### A.2.2 Output

C++ provides the output operator << to write character strings and the contents of variables whose data types are any of the fundamental ones. For example, the program segment

```
int count = 5;
double average = 20.3;
cout << "The average of the " << count
     << " distances read is " << average
     << " miles.\n";
```

produces the output: The average of the 5 distances read is 20.3 miles.

Like the input operator, the output operator is left-associative. Thus, the following output:

```
cout << "The average of the " << count
     << " distances read is " << average
     << " miles.\n";
```

The average of the 5 distances read is 20.3 miles.

Note that the output operator does not automatically insert whitespace, you must do so explicitly.

```
cout << "The average of the " << count
     << " distances read is " << average
     << " miles.\n";
```

The average of the 5 distances read is 20.3 miles.

### A.2.3 Manipulators

C++ enables you to gain more control over the format of your output than the input. Most of theseulators are listed in Figure A-4.

# 696 APPENDIX A Review of C++ Fundamentals

# FIGURE A-4 Stream manipulators

| Manipulator | Meaning |
|---|---|
| endl | Insert new line and flush |
| fixed | Use decimal point in floating-point output |
| left | Left-align output |
| right | Right-align output |
| scientific | Use exponential (e) notation in floating-point output |
| setfill(f) | Set fill character to f |
| setprecision(n) | Set floating-point precision to n |
| setw(n) | Set field width to n |
| showpoint | Show decimal point in floating-point output |
| showpos | Show + with positive integers |
| ws | Extract whitespace |

Even if you use the showpoint manipulator, gpa will likely appear as 4.0000 instead of 4.0. You can specify the number of digits that appear to the right of the decimal point by using the manipulator function setprecision, and you can insert a new-line character and flush the output stream by using the manipulator endl. Thus,

```
cout << showpoint;
cout << setprecision(1) << gpa << endl;
```

displays 4.0 by a carriage return.

The effect of setprecision on the output stream remains unchanged. Except for setprecision, a manipulator affects the appearance of the next characters on which (<< or >>)) operates. For example,

```
cout << right; // Right-align output
cout << "abc" << setw(6) << "def" << "ghi";
```

displays
abc defghi

## A.3 Functions

C++ program is a
collection of functions

As mentioned earlier in this appendix, a C++ program is a collection of functions. Usually, each function should perform one well-defined task. For example, the following function returns the largest of two integers:

A function definition
implements a
function's task

```
int computeMax(int x, int y)
{
    if (x > y)
        return x;
    else
        return y;
} // end computeMax
```

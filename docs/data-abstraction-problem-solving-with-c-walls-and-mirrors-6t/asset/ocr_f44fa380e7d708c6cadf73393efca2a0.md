The operators ++ and -- are useful for incrementing and decrementing a variable

Two more operators, ++ and --, provide convenient incrementing and decrementing operations:

```
a++ means a += 1, which means a = a + 1
```

Similarly,

```
a-- means a -= 1, which means a = a - 1
```

The operators ++ and -- can either follow their operands, as you just saw, or precede them. Although ++a, for instance, has the same effect as a++, the results differ when the operations are combined with assignment. For example,

```
b = ++a means a = a + 1; b = a
```

Here, the ++ operator acts on a before assigning a's new value to b. In contrast,

```
b = a++ means b = a; a = a + 1
```

The assignment operator assigns a's old value to b before the ++ operator acts on a. That is, the ++ operator acts on a after the assignment. The operators ++ and -- are often used within loops and with array indices, as you will see later in this appendix. When we use these operators with arithmetic variables, we write the operator after the variable.

In addition to the operators described here, C++ provides several other operators. A summary of all C++ operators and their precedences appears inside the cover of this book.

# A.2 Input and Output Using iostream

A typical C++ program reads its input from a keyboard and writes its output to a display. Such input and output consist of streams, which are simply sequences of characters that either come from or go to an input or output (I/O) device.

The data type of an input stream is istream, and the data type of an output stream is ostream.

The istream library provides these data types and three default stream variables: cin for the standard input stream, cout for the standard output stream, and cerr for the standard error stream, which also is an output stream. Your program gains access to the istream library by including the iostream header file. This section provides a brief introduction to simple input and output.

# A.2.1 Input

C++ provides the input operator >> to read integers, floating-point numbers, and characters into variables whose data types are any of the fundamental data types. The input operator has the input stream as its left operand and the variable that will contain the value read as its right operand. Thus,

The input operator >> reads from an input stream

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

That is, both of these expressions read characters for x from the input stream and then read subsequent characters for y.
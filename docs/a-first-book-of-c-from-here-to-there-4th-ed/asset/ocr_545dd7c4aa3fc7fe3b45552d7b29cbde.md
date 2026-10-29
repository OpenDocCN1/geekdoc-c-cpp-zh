```
cout << "The smallest long integer value is " << LONG_MIN << endl;
cout << "The largest long integer value is " << LONG_MAX << endl;
cout << sizeof(long) << " byte(s) are used to store long integers\n";

return 0;
}
```

Program 2.5 produces the following output:

```
The smallest character code is -128
The largest character code is 127
1 byte(s) are used to store characters

The smallest integer value is -2147483648
The largest integer value is 2147483647
4 byte(s) are used to store integers

The smallest short integer value is -32768
The largest short integer value is 32767
2 byte(s) are used to store short integers

The smallest long integer value is -2147483648
The largest long integer value is 2147483647
4 byte(s) are used to store long integers
```

Notice that the displayed values correspond with those listed previously in Table 2.9.

# Binary, Hexadecimal, and Octal Numbers

The most common binary number code for storing integer values in a computer is called the twos complement representation. With this code, the integer decimal equivalent of any bit pattern, such as 10001101, is easy to determine and can be found for positive or negative integers with no change in the conversion method. For convenience, assume byte-sized bit patterns consisting of 8 bits each, although the procedure carries over to larger bit patterns.

The easiest way to determine the decimal integer each bit pattern represents is to construct a simple device called a value box. Figure 2.8 shows a value box for a single byte. Mathematically, each value in this box represents an increasing power of 2. Because twos complement numbers must be capable of representing both positive and negative integers, the leftmost position, in addition to having the largest absolute magnitude, has a negative sign.

![](bbox=[0.32, 0.96, 0.88, 1.0])
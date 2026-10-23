```
```
scala> 53.toOctalString
res21: String = 65
```
```

To go the other way, from octal to binary, we simply convert the octal digits to three digit binary numbers. So the octal value, 3726 converts to 0111111010110. We can emphasize the groupings of bits by spacing them out: 011 111 010 110.

Moving between hexadecimal and binary is similarly simple. The only catch is that now a single digit needs to have 16 possible values. So the 0–9 that we used to will not suffice. It is typical to augment the normal digits with the letters A–F where A is ten and F is fifteen. Because $16 = 2^4$, we use groups of 4 bits when converting between hexadecimal and binary. Once again, you start the process with the lower bits and work up. So 110101 becomes 35. The large number you got from octal above, 0111 1101 0110 becomes 7D6 in hex. Again, there is a method called toHexString that can be used on the numeric types to quickly get the hexadecimal representation of a number.

While toOctalString and toHexString give us octal and hexadecimal representations of numeric values that we have in decimal, it is sometimes helpful to be able to enter values into programs using octal or hexadecimal. It is possible to enter literals in Scala using these bases. To get an octal literal, prefix the number with a leading zero. To get a hexadecimal literal, prefix it with 0x. The following uses of this confirm the conversions that we did for the larger number above.

```
```
scala> 03726.toBinaryString
res23: String = 11111010110

scala> 0x7D6.toBinaryString
res24: String = 11111010110
```
```

Values in hex or octal are particularly significant when you want to make sure that you know how many bits will be in the binary representation of the number.

# 3.4.5 Non-Integer Numbers

You now have a rather complete description of the integer number types and how they are represented in the machine. What about non-integer numeric values? We saw previously that if we type in a numeric value that includes a decimal point Scala tells us that it has type Double. The Double literal format is more powerful than just including decimal points. It also allows you to use scientific notation to enter very large or very small numbers. Simply follow a number by an e and the power of ten it should be multiplied by. So 15000.0 can also be written as 1.5e4.

The name Double is short for double precision floating point number. The full name includes information about the way that these numbers are stored in the memory of a computer. Like all values in a computer, the Double is stored as a collection of bits. To be specific, a Double uses 64-bits. This size is related to the double precision part. There is another type called Float that is a single precision floating point number and only uses 32-bits. In both cases, the internal representation uses floating point format. In many ways, this is similar to scientific notation, but in binary instead of decimal. The bits in a floating point number are grouped into three different parts. We will call them s, e, and m and the value of the number is given by $(-1)^s * (1+m) * 2^{(e-bias)}$. The first bit in the number is the sign bit, s. When that bit is on, the number is negative and when it is off it is positive. After the sign bit is a group of bits for the EXPONENT, e. Instead of using two’s compliment for determining if the exponent is negative, the exponent is biased by a value that is picked to match with the number of bits in the exponent. Using a bias instead of two’s compliment
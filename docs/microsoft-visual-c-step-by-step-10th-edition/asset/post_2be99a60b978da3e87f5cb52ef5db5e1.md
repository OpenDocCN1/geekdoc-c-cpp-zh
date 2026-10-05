
You normally use an int to hold an integer value. Internally, an int stores its value as a sequence of 32 bits, where each bit can be 0 or 1. Most of the time, you don't care about this internal binary representation; you just use an int type as a container to hold an integer value. Sometimes, however, programmers use the int type for other purposes. For example, some programs use an int as a set of binary flags and manipulate the individual bits within an int. If you're an old C hack like I am, what follows feel very familiar.

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_595_0.png)

To make a life little easier for handling data that you want to treat as a collection of binary values, C# enables you to specify integer constants using binary notation. You indicate that a constant should be treated as a binary representation by prefixing it with 0b0. For example, the following code assigns the binary value 1111 (15 in decimal) to a variable:

```uint
uint binData = 0b01111;
```

Note that this is a 4-bit value, but an integer occupies 32 bits. Any bits specified are initialized to 0. You should also observe that when you specify an integer as a binary value, it's good practice to store the result as an unsigned int (uint). In fact, if you provide a full 32-bit binary value, the C# compiler will insist that you use a uint.

To help cope with long strings of bits, you can also insert the underscore (_) character as a separator between blocks of digits, like this:

Click here to view code image

```uint
uint moreBinData = 0b_01110000_01010110_11001100_00001111;
```

In this example, the _ separator is used to mark the byte boundaries (32 bits is 4 bytes). You can use the _ separator anywhere within a binary constant (not just on byte boundaries); it is ignored by the C# compiler and is simply to help improve the readability of your code.

If you find binary strings a little lenny, you can opt to specify values using hexadecimal (base 16) notation by using the 0x prefix. The following two statements assign the same values shown in the previous example to another pair of variables. Again, you can use the _ character as a separator to make the values easier to read:

Click here to view code image

```uint
uint hexData = 0x0_;
uint moreHexData = 0x0_F0_5A_CC_0F;
```

# Displaying binary values

If you need to display the binary representation of an integer, you can use the ToString method. Convert.ToString is a heavily overloaded method that can generate a string representation of a range of data values held in different types. If you're converting integer data, you can additionally specify a numeric base (2, 8, 10, or 16), and the method will convert the integer to that base using an algorithm a little like the exercises you've seen in some earlier chapters. The following example prints the binary value of the moreHexData:

Click here to view code image

```uint
uint moreHexData = 0x0_F0_5A_CC_0F;
Console.WriteLine("Convert.ToString(moreHexData, 2)");
// displays 11110000010101101100110000111
```

# Manipulating binary values

C# provides a set of operators that you can use to access and manipulate the individual bits in an uint. These operators are as follows:

- The not (~) operator: This is a unary operator that performs a bitwise complement. For example, if you apply the ~ operator to the 8-bit value 0b_11001100 (204 decimal), you obtain the result 0b_00110011 (51 decimal). All the ones in the original value become zeros, and all the zeros become ones.

> ### ### Note
> The examples shown here are purely illustrative and are accurate only to 8 bits. In C#, the int type is 32 bits, so if you try any of these examples in a C# application, you will get a 32-bit result that might be different from those shown in this list. For example, in 32 bits, 204 is 0b_00000000_00000000_00001100, so in C#, ~204 is 0b_11111111_11111111_11001100 (which is actually -205 in C#).

- The left-shift (<<) operator: This is a binary operator that performs a left shift. The 8-bit expression 204 << 2 returns the value 48. (In binary, 48 is 0b_00110000, and shifting it by two places far-left bits are discarded, and zeros are introduced from the right. There is a corresponding right-shift operator (>>)).

- The OR (|) operator: This is a binary operator that performs a bitwise OR operation, returning a value containing a one in each position where either of the operands has a one. For example, the 8-bit expression 204 | 24 has the value 220 (204 is 0b_11001100, 24 is 0b_00010000, and 220 is 0b_11011100).

- The AND (&) operator: This operator performs a bitwise AND operation. It is similar to the bitwise OR operator, but it returns a value containing a one in each position where both of the operands have a one. So, the 8-bit expression 204 & 24 is 8 (204 is 0b_11001100, 24 is 0b_00010000, and 8 is 0b_00001000).

- The XOR (^) operator: This operator performs a bitwise exclusive OR operation, returning a one in each bit where there is a one in operand or the other but not. (Two ones yield a zero; this is the “exclusive” part of the operator.) The 8-bit expression 204 ^ 24 is 228 (204 is 0b_11001100, 24 is 0b_00010000, and 228 is 0b_11101100).

The trouble with these examples is that although they work, they are fiendishly difficult to understand. They’re complicated, and the solution is a very low-level one: it fails to create an abstraction of the problem that solves, and it’s consequently very difficult to maintain code that performs these kinds of operations.

# Solving the same problems using indexers

Let’s pull back from the preceding low-level solution for a moment and remember what the problem is: you'd like to use an int as an array of bits. Therefore, the best way to solve this problem is to use an int as if it were an array. For instance, to gain access and write a binary value to one of the six positions in the bits variable, from the right, use an expression such as the following (remember that arrays start with index 0):

```uint
bits[5];
```

And, to set the bit four places from the right to true, you'd like to be able to write this:

Click here to view code image

```uint
bits[3] = true; // currently invalid code
```

> ### ### Note
> To seasoned C developers, the Boolean value true is synonymous with the binary value 1, and the Boolean value false is synonymous with the binary value 0. Consequently, in C, the expression bits[3] = true means “Set the bit four places from the right of the bits variable is variable to 1."

Unfortunately, you can't use the square bracket notation on an int; it works only on an array or a type that behaves like an array. So, the solution to the problem is to create a new type that acts, feels, and is used like an array of bool variables but is implemented by using an int. You can achieve this feat by defining an indexer.


## Chapter 26
C quick reference

Make use of these handy cheat sheets and code examples

## Control Structures

```
if (<test>)
    <code executed if test is true>
```

```
if (<test>)
    <code executed if test is true>
else
    <code executed if test is false>
```

```
if (<test1>)
    <code executed if test1 is true>
else if (<test2>)
    <code executed if test1 is false and test2 is true>
else
    <code executed if test1 is false and test2 is false>
```

```
switch (<variable>)
{
    case <testval1> : <code executed if variable is testval1>
        break;
    case <testval2> : <code executed if variable is testval2>
        break;
```

```
default : <code executed if variable is neither testval1 nor testval2>
break;
```

```
}
```

```
switch (<variable>)
{
case <testval1> : <code executed if variable is testval1>
case <testval2> : <code executed if variable is either testval1 or testval2>
break;
default : <code executed if variable is neither testval1 nor testval2>
break;
```

```
}
```

```
while (<test>)
<code executed repeatedly while test is true>
```

```
do
<code executed once and then repeatedly while test is true>
while (<test>);
```

```
for (<initial condition>; <increment>; <termination condition>)
<code executed repeatedly until termination condition
is true>
```

In all loops, the keyword break can be used to exit the loop and resume execution immediately after the loop.

In all loops, the keyword continue can be used to skip code remaining in the body of the loop and resume execution at the next iteration of the loop test.

## Variable Types

| Name | Description | Size |
|---|---|--|
| char | Single alphanumeric character | 1 |
| signed char | Signed 8-bit integer (-128 - 127) | 1 |
| unsigned char | Unsigned 8-bit integer (0 - 255) | 1 |
| short, signed short | Signed 16-bit integer (-32768 - 32767) | 2 |
| unsigned short | Unsigned 16-bit integer (0 - 65535) | 2 |
| int, signed int | Signed 32-bit integer (-2147483648 - 2147483647) | 4 |
| unsigned int | Unsigned 32-bit integer (0 - 4294967295) | 4 |
| long, signed long | Signed 32-bit integer (-2147483648 - 2147483647) | 4 |
| unsigned long | Unsigned 32-bit integer (0 - 4294967295) | 4 |
| float | Floating-point value (+/- 3.402823 x 10^38) | 4 |
| double | Double-precision floating-point value (+/- 10^308) | 8 |

Dependent on platform, int can be either a short (16 bits) or a long (32 bits), on Raspian, as per the table above, int is a long (32 bit) integer value.

## Format Specifiers

| Specifier | Format / Type |
|---|--|
| %c | Alphanumeric character / char |
| %d | Signed decimal value / int |
| %ld | Signed decimal value / long int |

## INTRODUCTION TO C AND C++ PROGRAMMING

```
%u Unsigned decimal value / int
%lu Unsigned decimal value / long int
%o Octal value / int
%lo Octal value / long int
%x, %X Hexadecimal value / int
%lx, %lX Hexadecimal value / long int
%f Floating-point value / float
%e Exponential value / float
```

* %x displays a value as a hexadecimal with lower-case letters through f; %X displays it with upper-case letters A through F.

The width (or minimum number of characters printed) can be set by inserting a number between the % and the letter; this will pad a value shorter than with spaces at the start. To pad with spaces at the end, insert a - between the % and the number. To pad with leading zeroes, insert a 0 between the % and the number.

For example, to print an integer variable with the value 42, using the format specifier `%5d` will print 42 with three spaces before it. The format specifier `-5d` will print 42 with three spaces after it. The format specifier `%05d` will print it as 00042.

The number of decimal places shown for a floating-point or exponential value can be set by inserting a decimal point followed by a number between the % and the letter, this can be combined with a width by putting the width before the decimal point.

For example, to print a floating-point variable with the value 76.54321, the format specifier `%.2f` will print it as 76.54. The format specifier `%0.2f` will print it as 00076.54 (Note that the decimal point takes up one character of the specified width)

## Operators

The operators in the table below produce a result which can be assigned to another variable, e.g. c = a + b, but do not affect the values of a or b.

| Symbol | Function |
|---|---|
| a + b | Addition |
| a - b | Subtraction |
| a * b | Multiplication |
| a / b | Division |
| a % b | Modulo (remainder of a / b) |
| a & b | Bitwise AND |
| a | b | Bitwise OR |
| a ^ b | Bitwise XOR |
| a << b | Bit shift left |
| a >> b | Bit shift right |
| ~a | Bitwise 1's complement |
| !a | Logical NOT |

The operators in the table below modify the value of a directly.

| Symbol | Function |
|---|---|
| a++ | Increment a by one |
| a-- | Decrement a by one |
| ++a | Increment a by one |

## AN INTRODUCTION TO C AND PROGRAMMING

a-- | Decrement a by one
a += b | Increment a by b
a -= b | Decrement a by b
a *= b | Multiply a by b
a /= b | Divide a by b
a %= b | remainder of a / b
a &= b | Bitwise AND with b
a |= b | Bitwise OR with b
a ^= b | Bitwise XOR with b
a <<= b | Bit shift left by b
a >>= b | Bit shift right by b

2. The difference between a++ and ++a is that they are used in a test, such as if (a++), a++ tests the value and increments it, while ++a increments the value first and then tests it.

The operators in the table below are used for comparisons.

| Symbol | Function |
|---|---|
| == | Is equal to |
| != | Is not equal to |
| > | Is greater than |
| < | Is less than |
| >= | Is greater than or equal to |
| <= | Is less than or equal to |

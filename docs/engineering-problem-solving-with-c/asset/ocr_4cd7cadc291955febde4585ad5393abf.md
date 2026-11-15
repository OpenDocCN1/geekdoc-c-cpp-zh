The use of parentheses in the second statement is not required, but is used for readability. Consider this assignment statement:

```
x = x + 1 ;
```

In algebra, this is invalid because a value cannot be equal to itself plus 1. However, this assignment statement should not be read as an equality; instead, it should be read as x is assigned the value of x plus 1. With this interpretation, the statement indicates that the value stored in the object x is incremented by 1. Thus, if the value of x is 5 before this statement is executed, then the value of x will be 6 after the statement is executed.

C++ also includes a modulus operator % that is used to compute the remainder in a division between two integers. For example, 5%2 is equal to 1, 6%3 is equal to 0, and 2%7 is equal to 2. (The quotient of 2/7 is zero with a remainder of 2.) If a and b are integers, then the expression a/b computes the integer quotient, whereas the expression a%b computes the integer remainder. Thus, if a is equal to 9 and b is equal to 4, the value of a/b is 2 and the value of a%b is 1. If the value of b is equal to zero in either a/b or a%b, or if either of the integer values in a and b is negative in a%b, the result is system-dependent.

The modulus operator is useful in determining whether an integer is a multiple of another number. For example, if a%2 is equal to zero, then a is even; otherwise, a is odd. If a%5 is equal to zero, then a is a multiple of 5. We will use the modulus operator frequently in the development of engineering solutions.

The five operators (+, -, *, /, %) discussed in the previous paragraphs are binary operators—operators that operate on two operands (values). C++ also includes unary operators—operators that operate on a single operand. For example, plus and minus signs can be unary operators when they are used in an expression such as -x.

The result of a binary operation with values of the same type is another value of the same type. For example, if a and b are double values, then the result of a/b is also a double value. Similarly, if a and b are integers, then the result of a/b is also an integer; however, an integer division can sometimes produce unexpected results because any decimal portion of the integer division is dropped; the result is a truncated result, not a rounded result. Thus, 5/3 evaluates to 1, and 3/6 evaluates to 0. Arithmetic operators for programmer-defined classes are not provided by the compiler, but can be defined by the programmer as class methods.

An operation between values with different types is a mixed operation. Before the operation is performed, the value with the lower type is converted or promoted to the higher type (as discussed in conversions within assignment statements), and thus the operation is performed with values of the same type. For example, if an operation is specified between an integer and a floating point, the integer will be promoted to a floating point before the operation is performed; the result will be a floating point.

Suppose that we want to compute the average of a set of integers. If the sum and the count of the integers have been stored in the integer objects sum and count, it would seem that the following statements should correctly compute the average:

```
int sum, count;
double average;
...
average = sum/count;
```

However, the division between two integers gives an integer result that is then promoted to a double value. Thus, if sum is 18, and count is 5, then the value assigned to average is 3.0, not 3.6. To compute this average correctly, we use a cast operator—a unary operator that

| Precedence Level | Operator | Operation | Associates |
|---|---|---|---|
| 1 | + | unary plus | R to L |
|  | - | unary minus |  |
| 2 | * | multiplication | L to R |
|  | / | division |  |
|  | % | remainder |  |
| 3 | + | addition | L to R |
|  | - | subtraction |  |
|  | + | string concatenation |  |
| 4 | = | assignment | R to L |

## FIGURE 2.4 Precedence among some of the Java operators

The parentheses used in expressions are actually operators themselves. Parentheses have a higher precedence than almost any other operator. Figure 2.4 shows a precedence table with the relationships between the arithmetic operators, parentheses, and the assignment operator. Appendix D includes a full precedence table showing all Java operators.

For an expression to be syntactically correct, the number of left parentheses must match the number of right parentheses and they must be properly nested. The following examples are not valid expressions:

```
result = ((19 + 8) % 3) - 4);  // not valid
result = (19 (+ 8 %) 3 - 4);  // not valid
```

Keep in mind that when a variable is referenced in an expression, its current value is used to perform the calculation. In the following assignment statement, the current value of the variable count is added to the current value of the variable total, and the result is stored in the variable sum:

```
sum = count + total;
```

The original value contained in sum before this assignment is overwritten by the calculated value. The values stored in count and total are not changed.

The same variable can appear on both the left-hand side and the right-hand side of an assignment statement. Suppose the current value of a variable called count is 15 when the following assignment statement is executed:

```
count = count + 1;
```

Because the right-hand expression is evaluated first, the original value of count is obtained and the value 1 is added to it, producing the result 16. That result is then stored in the variable count, overwriting the original value of 15 with the new value of 16. Therefore, this assignment statement increments, or adds 1 to, the variable count.

Let’s look at another example of expression processing. The program in Listing 2.7, called TempConverter, converts a particular Celsius temperature value to its equivalent Fahrenheit value using an expression that computes the following formula:

Fahrenheit = 9/5 Celsius + 32

### LISTING 2.7

```
//************************************************************************
// TempConverter.java      Author: Lewis/Loftus
//
// Demonstrates the use of primitive data types and arithmetic
// expressions.
//************************************************************************

public class TempConverter
{
    //-------------------------------------------------------------
    // Computes the Fahrenheit equivalent of a specific Celsius
    // value using the formula F = (9/5)C + 32.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        final int BASE = 32;
        final double CONVERSION_FACTOR = 9.0 / 5.0;

        double fahrenheitTemp;
        int celsiusTemp = 24;  // value to convert

        fahrenheitTemp = celsiusTemp * CONVERSION_FACTOR + BASE;

        System.out.println ("Celsius Temperature: " + celsiusTemp);
        System.out.println ("Fahrenheit Equivalent: " + fahrenheitTemp);
    }
}
```

### OUTPUT

Celsius Temperature: 24
Fahrenheit Equivalent: 75.2

Note that in the temperature conversion program, the operands to the division operation are floating point literals to ensure that the fractional part of the number is kept. The precedence rules dictate that the multiplication happens before the addition in the final conversion computation.

The TempConverter program is not very useful because it converts only one data value that we included in the program as a constant (24 degrees Celsius). Every time the program is run it produces the same result. A far more useful version of the program would obtain the value to be converted from the user each time the program is executed. Interactive programs that read user input are discussed later in this chapter.

## Increment and Decrement Operators

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
count currently contains the value 15, the following statement assigns the value 15 to total and the value 16 to count:

```
total = count++;
```

However, the following statement assigns the value 16 to both total and count:

```
total = ++count;
```

The value of count is incremented in both situations, but the value used in the larger expression depends on whether a prefix or postfix form of the increment operator is used.

Because of the subtle differences between the prefix and postfix forms of the increment and decrement operators, they should be used with care. As always, favor the side of readability.

## Assignment Operators

As a convenience, several assignment operators have been defined in Java that combine a basic operation with assignment. For example, the += operator can be used as follows:

```
total += 5;
```

This performs the same operation as the following statement:

```
total = total + 5;
```

The right-hand side of the assignment operator can be a full expression. The expression on the right-hand side of the operator is evaluated, then that result is added to the current value of the variable on the left-hand side, and that value is stored in the variable. Therefore, the following statement:

```
total += (sum - 12) / count;
```

is equivalent to:

```
total = total + ((sum - 12) / count);
```

Many similar assignment operators are defined in Java, including those that perform subtraction (-=), multiplication (*=), division (/=), and remainder (%=). The entire set of Java operators is discussed in Appendix D.

All of the assignment operators evaluate the entire expression on the right-hand side first, then use the result as the right operand of the other operation. Therefore, the following statement:

```
result *= count1 + count2;
```

is equivalent to:

```
result = result * (count1 + count2);
```

Likewise, the following statement:

```
result %= (highest - 40) / 2;
```

is equivalent to:

```
result = result % ((highest - 40) / 2);
```

Some assignment operators perform particular functions depending on the types of the operands, just as their corresponding regular operators do. For example, if the operands to the += operator are strings, then the assignment operator performs string concatenation.

## SELF-REVIEW QUESTIONS (see answers in Appendix N)

- SR 2.21 What is the result of 19%5 when evaluated in a Java expression? Explain.

- SR 2.22 What is the result of 13/4 when evaluated in a Java expression? Explain.

- SR 2.23 If an integer variable diameter currently holds the value 5, what is its value after the following statement is executed? Explain.
  
  diameter = diameter * 4;

- SR 2.24 What is operator precedence?

- SR 2.25 What is the value of each of the following expressions?
  - a. 15 + 7 * 3
  - b. (15 + 7) * 3
  - c. 3 * 6 + 10 / 5 + 5
  - d. 27 % 5 + 7 % 3
  - e. 100 / 2 / 2 / 2
  - f. 100 / ( 2 / 2 ) / 2

- SR 2.26 For each of the following expressions state whether they are valid or invalid. If invalid, explain why.
  - a. result = ( 5 + 2 );
  - b. result = ( 5 + 2 * ( 15 - 3 );
  - c. result = ( 5 + 2 (;
  - d. result = ( 5 + 2 ( 4 ) );

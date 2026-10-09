Using the minus operator is equivalent to subtracting the operand from zero.

The unary plus operator (+) rarely2 has any effect on a value. It is a superfluous addition to the C# language and was included for the sake of symmetry.

# Arithmetic Binary Operators ( + , - , * , / , % )

Binary operators require two operands. C# uses infix notation for binary operators: The operator appears between the left and right operands. The result of every binary operator other than assignment must be used somehow—for example, by using it as an operand in another expression such as an assignment.

> **Language Contrast: C++—Operator-Only Statements**

In contrast to the rule mentioned previously, C++ will allow a single binary expression to form the entirety of a statement, such as `4+5;`, to compile. In C#, only assignment, call, increment, decrement, await, and object creation expressions are allowed to be the entirety of a statement.

The subtraction example in Listing 4.3 illustrates the use of a binary operator—more specifically, an arithmetic binary operator. The operands appear on each side of the arithmetic operator, and then the calculated value is assigned. The other arithmetic binary operators are addition (+), division (/), multiplication (*), and remainder (% [sometimes called the mod operator]).

# **LISTING 4.3: Using Binary Operators**

```
class Division
{
    static void Main()
    {
        int numerator;
        int denominator;
        int quotient;
        int remainder;
```

2. The unary + operator is defined to take operands of type int, uint, long, ulong, float, double, and decimal (and nullable versions of those types) Using it on other numeric types such as short will convert its operand to one of these types as appropriate.
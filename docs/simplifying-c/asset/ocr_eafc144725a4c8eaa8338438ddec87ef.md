Each of the operators shown in Figure 1 is used to form an expression in C language. The next section discusses about these operators in detail along with their usage.

# Arithmetic Operators

C language provides different operators, such as +, -., *, /, and %, to perform arithmetic operations. Table 1 lists the various operator symbols, their name, and their usage:

Table 1: Arithmetic Operators
| Symbol | Name | Usage |
| --- | --- | --- |
| + | Addition operator | Add two operands; Unary plus |
| − | Subtraction operator | Subtract two operands; Unary minus |
| * | Multiplication operator | Multiply two operand |
| / | Division operator | Quotient of division of two operands |
| % | Modulo operator | Remainder of division of two operands |

The first four operators listed in Table 1 are used in most of the mathematical expressions. C language provides us with an additional operator % known as modulo operator. It is used to get a remainder when performing division of two operands. The operands can be a variable or a constant. Let us now see how we can use these operators in an expression. For example, consider the following C statement:

```
i_area = i_length * i_breadth;
```

shown in Figure 2. This statement is called a binary C expression, where i_area, i_length, and i_breadth are known as C identifiers or variables. The reason it is known as binary C expression is that it consists of an expression of the form operand 1 operator operand 2. Operand 1 will always be a single value, but operand 2 can be another expression or a constant value. The example statement, when executed, results in two operations, as shown in Figure 2:

![](bbox=[0.27, 0.64, 0.79, 0.77])

Figure 2 shows that first the two operands, i.e., i_length and i_breadth, are multiplied, and then the result of the multiplication is assigned to i_area. Thus, an expression in C can result into multiple operations.
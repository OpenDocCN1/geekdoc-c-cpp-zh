NOTE Readability is very important when you write code. Always place a space before and after every arithmetic operator, including the equal symbol ( = ). The compiler ignores the white space, but readers of your code appreciate it.

# TABLE 2-12 Basic arithmetic operators

| Operator | Operation |
|---|---|
| + | Addition |
| - | Subtraction |
| * | Multiplication |
| / | Division |
| % | Modulus |

The modulus operator (%) is sometimes referred to as the remainder operator. In most languages, both operands must be of integral type. C# allows you to use floating-point values as operands and the modulus operator. The result produced is the remainder of operand1 divided by operand2. Given the following statements, Figure 2-8 illustrates the results.

```
int firstValue = 67;
int secondValue = 3;
int result;
result = firstValue % secondValue;
```

![](bbox=[0.28, 0.84, 0.88, 0.96])

# FIGURE 2-8 Result of 67 % 3
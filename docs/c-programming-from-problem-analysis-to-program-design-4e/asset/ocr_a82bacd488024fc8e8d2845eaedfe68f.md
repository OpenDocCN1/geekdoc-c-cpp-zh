# Increment and Decrement Operations

A common arithmetic operation is to add or subtract the number one (1) to or from a memory location. Increment/decrement operators are used for this. C#, like C++ and Java, has a special unary operator that increments and decrements by one. It is considered a unary operator because it requires a single operand. The basic operators explored in the preceding explanations are all binary operators that require two operands.

The symbols used for increment and decrement are ++ and --. No space is permitted between the two symbols (++ or --).

```
num++;
    // could be written as num = num + 1;
--value1;
    // could be written as value1 = value1 - 1;
```

The first statement adds 1 to num. The second subtracts 1 from value1. The increment and decrement operators are often used in situations in which a counter is needed. They are not used to accumulate values, because they always add one or subtract one from the variable.

NOTE
In C#, when you use the increment and decrement operators with floating-point types, no syntax error is generated. C# adds or subtracts the number 1 to the variable. You can also use the ++ or -- with a variable of char type.

If you use these operators in an arithmetic expression involving additional operands, the placement of the ++ or -- is important. If they appear as prefixes, or to the left of the variable, the increment or decrement is performed before using them in the expression. When placed before the operand, they are called preincrement or predecrement operators; when placed after the operand, they are called postincrement or postdecrement operators. For example, if the following declaration were made and then each of the WriteLine() methods were called, the output for Example 2-11 would be:

+   100
+   101
+   102

# EXAMPLE 2.11

```
int num = 100;
Console.WriteLine(num++);            // Displays 100
System.Console.WriteLine(num);          // Displays 101 after the post
                                        // increment is performed on the
                                        // previous line
Console.WriteLine(++num);               // Displays 102
```

With Example 2-11, the last value printed is 102. If num were used following the lines of code in the example, num has a value of 102. Notice that the incremented value is displayed here
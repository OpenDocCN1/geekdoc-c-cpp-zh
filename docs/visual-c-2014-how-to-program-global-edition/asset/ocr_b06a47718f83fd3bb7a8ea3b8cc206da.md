# Chapter 5 Algorithm Development and Control Statements: Part I

| Operator | expression | Explanation |
|---|---|--|
| ++ (prefix increment) | ++a | Increments a by 1 and uses the new value of a in the expression in which a resides. |
| ++ (postfix increment) | a++ | Increments a by 1, but uses the original value of a in the expression in which a resides. |
| -- (prefix decrement) | --b | Decrements b by 1 and uses the new value of b in the expression in which b resides. |
| -- (postfix decrement) | b-- | Decrements b by 1 but uses the original value of b in the expression in which b resides.

**Fig. 5.15** Increment and decrement operators.

Using the postfix increment (or decrement) operator to add 1 (or subtract 1 from) a variable is known as postincrementing (or postdecrementing). This causes the current value of the variable to be used in the expression in which it appears; the variable's value is incremented (decremented) by 1.

> > Good Programming Practice 5.4: Unlike binary operators, the unary increment and decrement operators as a matter of style should be placed next to their operands, with no intervening spacing.

# 5.13.1 Prefix Increment vs. Postfix Increment

Figure 5.16 demonstrates the difference between the prefix-increment and postfix-increment versions of the ++ operator. The decrement operator (--) works similarly.

```
// Increment.cs
// Prefix increment and postfix increment operators.
using System;
class Increment {
    static void Main() {
        // demonstrate postfix increment operator
        int c = 5; // assign 5 to c
        Console.WriteLine($"c before postincrement: {c}"); // displays 5
        Console.WriteLine($"c postincrement: {c++}"); // displays 5
        Console.WriteLine($"c c after postincrement: {c}"); // displays 6
```

**Fig. 5.16** Prefix-increment and postfix-increment operators. (Part I of 2.)
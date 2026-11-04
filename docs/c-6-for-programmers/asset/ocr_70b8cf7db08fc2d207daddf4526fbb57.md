# Good Programming Practice 5.2

Unlike binary operators, the unary increment and decrement operators as a matter of style should be placed next to their operands, with no intervening spaces.

# 5.11.1 Prefix Increment vs. Postfix Increment

Figure 5.12 demonstrates the difference between the prefix-increment and postfix-increment versions of the ++ increment operator. The decrement operator (--) works similarly.

```
// Fig. 5.12: Increment.cs
// Prefix-increment and postfix-increment operators.
using System;

class Increment
{
    static void Main()
    {
        // demonstrate postfix increment operator
        int c = 5; // assign 5 to c
        Console.WriteLine("c before postincrement: {0}", c); // displays 5
        Console.WriteLine("postincrementing c: {0}", c++); // displays 5
        Console.WriteLine("c after postincrement: {0}", c); // displays 6

        Console.WriteLine(); // skip a line

        // demonstrate prefix increment operator
        c = 5; // assign 5 to c
        Console.WriteLine("c before preincrement: {0}", c); // displays 5
        Console.WriteLine("preincrementing c: {0}", ++c); // displays 6
        Console.WriteLine("c after preincrement: {0}", c); // displays 6
    }
}
```

c before postincrement: 5
postincrementing c: 5
c after postincrement: 6

c before preincrement: 5
preincrementing c: 6
c after preincrement: 6

Fig. 5.12 | Prefix-increment and postfix-increment operators.

Line 10 initializes the variable c to 5, and line 11 outputs c's initial value. Line 12 outputs the value of the expression c++. This expression postincrements the variable c, so c's original value (5) is output, then c's value is incremented (to 6). Thus, line 12 outputs c's initial value (5) again. Line 13 outputs c's new value (6) to prove that the variable's value was indeed incremented in line 12.
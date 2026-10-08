# 6.11 Logical Operators 255

# Software Engineering Observation 6.2

There's a tension between achieving quality software engineering and achieving the best-performing software. Often, one of these goals is achieved at the expense of the other. For all the most-intensive situations, apply the following rule: First, make your code simple and correct; then make it fast, but only if necessary.

![](bbox=[0.153, 0.105, 0.209, 0.153])

```
// Fig. 6.14: ContinueTest.cs
// continue statement skipping an iteration of a for statement
using System;
class ContinueTest {
    static void Main() {
        for (int count = 1; count <= 10; ++count) // loop 10 times {
            if (count == 5) // if count is 5 {
                continue; // skip remaining code in loop
            }
            Console.Write($"{count}");
            Console.WriteLine("\nused continue to skip displaying 5");
        }
    }
```

1 2 3 4 6 7 8 9 10
Used continue to skip displaying 5

Fig. 6.14 | continue statement skipping an iteration of a for statement.

# 6.11 Logical Operators

The if, ...else, while, do...while and for statements each require a condition to determine how to continue an app's flow of control. For far, we've studied only simple conditions, such as count < 10, number=sentinelValue and total > 1000. Simple conditions are expressed in terms of the relational operators, >, <= and =, the equality operators are != and .. Each expression tests only one condition. To test multiple conditions in the process of making a decision, we performed these in separate statements or nested in if...else... statements require more complex conditions to determine an app's flow of control.

C# provides logical operators to enable you to form more complex conditions by combining conditions. The logical operators are && (boolean AND), || (conditional AND), | (boolean inclusive OR), ^ (exclusive OR) and ! (logical negation).
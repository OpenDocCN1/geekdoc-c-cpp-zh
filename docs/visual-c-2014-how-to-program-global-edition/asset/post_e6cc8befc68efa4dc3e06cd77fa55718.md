
## 236 Chapter 6 Control Statements: Part 2

## Common Programming Error 6.1

Using an incorrect relational operator or an incorrect final value of a loop counter in the loop-continuation condition of an iteration statement can cause an off-by-one error.

![](img/57baed2319be0bb1b5f98674846f2711_236_0.png)

## Error-Prevention Tip 6.2

Using the final value and operator <= in a loop's condition helps avoid off-by-one errors. For a loop that outputs 1 to 10, loop-continuation condition should be counter < 11 rather than counter < 10 (which causes an off-by-one error) or counter <= 11 (which is correct). Many programmers prefer zero-based counting in which, to count 10 times, you'd initialize counter to zero and use the loop-continuation test < 10.

### 6.3.1 A Closer Look at the Statement's Header

Figure 6.3 takes a closer look at the statement in Fig. 6.2. The first line—including the keyword for and everything in parentheses after (line 11 in Fig. 6.2)—is sometimes the for statement header. For header “does it all”—it specifies each item needed for counter-controlled iteration with a control variable.

![](img/57baed2319be0bb1b5f98674846f2711_236_1.png)

Fig. 6.3 | statement header components.

### 6.3.2 General Format of a Statement

The general format of for statement is

```
for (initialization; loopContinuationCondition; increment)
  statement
```

where the initialization expression names the loop's control variable and provides its initial value, the loopContinuationCondition determines whether looping should continue and the increment modifies the control variable's value (whether an increment or decrement), so that the loop-continuation condition eventually becomes false. The two semicolons in the for are required. We don't include a semicolon after statement, because the semicolon is already assumed to be included in the notion of a statement.

### 6.3.3 Scope of a Statement's Control Variable

If the initialization expression in for header declares the control variable (i.e., the control variable's type is specified before the variable name, as in Fig. 6.2), the control variable can be used *only* in that statement—it will not exist outside it. This restricted use of the name of the control variable is known as the *scope*. The scope of a variable defines where it can be used in an app. For example, a local variable can be used only in the method that declares it and *only* from the point of declaration through the end of the block in which the variable has been declared. Scope is discussed in detail in Chapter 7, Methods: A Deeper Look.

![](img/57baed2319be0bb1b5f98674846f2711_237_0.png)

### Programming Error 6.2
When a statement's control variable is declared in the initialization section of a *for*'s header, using the control variable after the *for*'s body is a compilation error.

### 6.3.4 Expressions in a For's Header Are Optional

All expressions in a header are optional. If the loop *ContinuationCondition* is omitted, C# assumes that it's *always true*, creating an infinite loop. You can omit the initialization expression if it initializes the control variable *before* the loop—in this case, the scope of the control variable will *not* be limited to the loop. You can omit the increment expression if the app increments in the loop's body or if no increment is needed. The increment expression in a for acts as if it were a standalone statement. Therefore, the expressions

```
counter = counter + 1
counter += 1
++counter
counter++
```

are equivalent increment expressions in a for statement. Many programmers prefer counter++ because it's concise and because a for evaluates after its body executes—so the postfix increment form *seems* more natural. In this case, the variable being incremented does not appear in a larger expression, so the prefix and postfix increment operators have the same effect.

![](img/57baed2319be0bb1b5f98674846f2711_237_1.png)

### Tip 6.1
There's a slight performance advantage to using the prefix increment operator, but if you choose the postfix increment operator because it seems more natural (as in a for header), optimizing compilers are likely to generate code that uses the more efficient for anyway.

![](img/57baed2319be0bb1b5f98674846f2711_237_2.png)

### Error-Prevention 6.3
Infinite loops occur when the loop-continuation condition in an iteration statement becomes false. To prevent this situation in a counter-controlled loop, ensure that the control variable is incremented (or decremented) during each iteration of the loop. In a sentinel-controlled loop, ensure that the sentinel value is eventually reached.

### 6.3.5 Placing Arithmetic Expressions in a for Statement's Header

The initialization, loop-continuation condition and increment portions of a for statement can contain arithmetic expressions. For example, assume that x = 2 and y = 10; if x and y are not modified in the body of the loop, the statement

```
for (int j = x; j <= 4 * y; j += y / x)
```

is equivalent to the statement

```
for (int j = 2; j <= 80; j += 5)
```

The increment of a for statement may be negative, in which case it's actually a decrement, and the loop counts downward.

### 6.3.6 Using a for Statement's Control Variable in the Statement's Body

Apps frequently display the control variable or use it in calculations in the loop body, but this is not required. The control variable is commonly used to control iteration without being mentioned in the body of the for.

> **Error-Prevention Tip 6.4**
The value of the control variable can be changed in the body of a for loop, avoid doing so, because this practice can lead to subtle errors. If a program must modify the control variable's value in the loop body, use while rather than for.

### 6.3.7 UML Activity Diagram for for Statement

Figure 6.4 shows the activity diagram for the for statement in Fig. 6.2. The diagram makes it clear that initialization occurs once—before the loop-continuation test—and that incrementing occurs after the body executes.

![](img/57baed2319be0bb1b5f98674846f2711_238_0.png)

Fig. 6.4 | UML diagram for for statement.

### 6.4 Examples Using the for Statement

The following examples show techniques for varying the control variable. In each case, we write only the for header.

### 6.5 App: Summing Integers

a) Vary the control variable from 1 to 100 in increments of 1.

```
for (int i = 1; i <= 100; ++i)
```

b) Vary the control variable from 100 to 1 in decrements.

```
for (int i = 100; i >= 1; --i)
```

c) Vary the control variable from 7 to 77 in increments of 7.

```
for (int i = 7; i <= 77; i += 7)
```

d) Vary the control variable from 20 to 2 in decrements.

```
for (int i = 20; i >= 2; i -= 2)
```

e) Vary the control variable over the sequence 2, 5, 8, 11, 14, 17, 20.

```
for (int i = 2; i <= 20; i += 3)
```

f) Vary the control variable over the sequence 99, 88, 77, 66, 55, 44, 33, 22, 11, 0.

```
for (int i = 99; i >= 0; i -= 11)
```

## Common Programming Error 6.3

Using an incorrect relational operator in the loop-continuation condition of a loop that counts down (e.g., using < 1 instead of >= 1 in a loop counting down to 1) would cause a logic error.

![](img/57baed2319be0bb1b5f98674846f2711_239_0.png)

## Common Programming Error 6.4

Do not use equality operators (! or ==) in a loop-continuation condition if the loop's control variable increments or decrements by more than 1. For example, consider the statement for (int counter = 1; counter += 2). The loop-continuation test (counter != 10) never becomes false (resulting in an infinite loop) because counter increases by 2 each iteration (and never becomes 10).

## 6.5 App: Summing Integers

We now consider a sample app that demonstrates a simple use of for. The app in Fig. 6.5 uses a statement to sum the even integers from 2 to 20 and store the result in an int variable total. Each iteration of the loop (lines 12–15) adds control variable number's value to variable total.

```
// Fig. 6.5: Sum.cs
// Summing integers with the for statement.
using System;
class Sum
{
    static void Main()
    {
        int total = 0; // initialize total
        for (int i = 2; i <= 20; i += 2)
        {
            total += i;
            Console.WriteLine(total);
        }
    }
}
```

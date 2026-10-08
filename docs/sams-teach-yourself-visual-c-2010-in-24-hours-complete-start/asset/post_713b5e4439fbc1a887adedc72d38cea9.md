
## Try It Yourself

### Working with the if Statement

To see how the if statement works, follow these steps. Keep Visual Studio open at the end of this exercise because you will use this application later.

- 1. Open the SelectionStatements project in Visual Studio.
- 2. Open Form1.cs by right-clicking the file and selecting the View Code context menu choice.
- 3. In the code editor, locate the method named CheckGuess, which looks like

    ```csharp
    private Result CheckGuess(decimal guess)
    {
        Result result;
        return result;
    }
    ```

- 4. Modify the CheckGuess method so that the appropriate value of Result is returned based on the number passed as the method argument.
- 5. Look at the buttonCheckGuess_Click method, examining the nested if statement it contains.
- 6. Run the application by pressing F5. Enter guesses and watch how the program responds based on your guess.

## The switch Statement

Switches can be thought of as the natural progression from cascaded if statements. They provide similar functionality but are more compact and flexible. The switch statement selects a statement list based on a label that corresponds to the value of the expression.

The syntax of a switch statement is

```csharp
switch (expression)
{
    case constant-expression :
        statement-list
        break;

    default :
        statement-list
        break;
}
```

The body of the switch is the **switch-block** and contains one or more switch-sections. Each switch-section contains at least one label followed by a statement-list.

The type of expression establishes the **governing type** of the switch and can be sbyte, byte, short, ushort, int, uint, long, ulong, char, the nullable version of those types, the string type, or an enumerated type. The expression is evaluated only once.

The label for a switch-section must be a constant expression that is unique within the same switch-block and be implicitly convertible to the governing type. For switches whose governing type is string or a nullable type, a case label of null is permitted.

### Switches on string

The evaluation of expression is case-sensitive, so a switch-section will only be executed if its label exactly matches.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_171_0.png)

If the value of expression matches one of the constants in a case label, control is transferred to the first statement after that label. If no matching case is found, control is transferred to the first statement after the default label, if present; otherwise, control is transferred to the next statement after the switch.

In Listing 7.3, if the condition (x == 0) or (x == 1) evaluates to true, the value of x displays; otherwise, "Invalid" displays.

### LISTING 7.3 A Simple switch Statement

```csharp
int x = 4;

switch (x)
{
    case 0:
        Console.WriteLine("x = " + x);
        break;

    case 1:
        Console.WriteLine("x = " + x);
        break;

    default:
        Console.WriteLine("Invalid");
        break;
}
```

You might have noticed that the code for case 0 and case 1 is identical. To eliminate this redundancy, you can provide a list of labels with no intervening statements.

## Fall Through

Unlike other programming languages, such as C and C++, switch statements in C# do not allow fall through of switch-sections, which occurs when execution starts in one switch-section and continues through to another switch-section.
To prevent fall-through, C# requires all switch-sections to end in a statement with an unreachable endpoint, of which an unconditional jump statement is one example. The most common is the break statement.
By not allowing such fall-through behavior, C# eliminates a common bug found in C and C++ programs and allows the order of the switch-sections to be changed without affecting the behavior of the statement.

Listing 7.4 shows the same switch statement from Listing 7.3 but uses case fall-through. Because there are no intervening statements, the “no fall-through rule” is not violated, and control is transferred to the first statement after the last label in the list.

### LISTING 7.4 A switch Statement Using Case Fall-Through

```csharp
int x = 4;
switch (x)
{
    case 0:
    case 1:
        Console.WriteLine("x = " + x);
        break;

    default:
        Console.WriteLine("Invalid");
        break;
}
```

## Scope

Scope within a switch statement is bounded by the entire switch-block, not each switch-section. This means that any local variables or constants declared inside a switch-section are local to the entire switch-block, not just that switch-section.
If you need to restrict scope to within a specific switch-section, you can create an additional nested scope by enclosing the statement list in curly braces.

## Try It Yourself

### Working with the switch Statement

To see how the switch statement works, follow these steps. If you closed Visual Studio, repeat the previous exercise first.

- 1. In the code editor, locate the method named `buttonCheckGuess_Click`. This method contains a nested *if* statement that determines which *Label* controls to display based upon the return value of the `CheckGuess` method.
- 2. Modify the `buttonCheckGuess_Click` method so that it uses a *switch* statement over the return value of the `CheckGuess` method rather than the nested *if* statements.
- 3. Run the application by pressing *F5*. Enter guesses and watch how the program responds based on your guess, which should be identical to the behavior from the previous exercise.

## Iteration Statements

Although selection statements enable one-time execution of a statement based on the value of an expression, iteration statements, also called **looping** statements, repeatedly execute the same statement. Iteration statements evaluate their expression each time, or **iteration**, through the loop. A **top-tested loop** evaluates the expression before the statement executes, whereas a **bottom-tested loop** evaluates the expression after the statement executes.

To terminate the loop early, without reevaluating the expression, you can use any of these jump statements: *break*, *goto*, *return*, or *throw*. The *continue* statement passes control to the next iteration.

### The while Statement

A *while* statement is a top-tested loop that repeatedly executes an embedded statement until the *boolean-expression* evaluates to *false*. Because the expression is evaluated before each iteration, the statement can be executed zero or more times.

The syntax for a *while* statement is

```csharp
while (*boolean-expression*)
    *embedded-statement*
```

If the result of evaluating *boolean-expression* is *true*, control is transferred to the *embedded-statement*. When the statement finishes executing, control is transferred to the start of the loop, where the expression is reevaluated.

If the result of evaluating *boolean-expression* is *false*, control is transferred to the next statement after the *while* statement. If the result of the *boolean-expression* is initially *false*, the *embedded-statement* never executes.

In Listing 7.5, the statements inside the body of the loop execute until i is greater than or equal to 10. If the i++; statement were not included in either the body of the loop or as part of the boolean-expression, the loop would execute forever.

### LISTING 7.5 The while Statement

```csharp
int i = 0;
while (i < 10)
{
    Console.WriteLine(i);
    i++;
}
```

## Try It Yourself

### Working with the while Statement

By following these steps, you see how the while statement works. Keep Visual Studio open at the end of this exercise because you will use this application later.

- 1. Open the *IterationStatements* project in Visual Studio.
- 2. Open *Form1.cs* right-clicking the file and selecting the **View Code** context menu choice.
- 3. In the code editor, modify the `PowersOfTwoWhileLoop` method so that it executes the following statements in a while loop.
    ```csharp
    this.textBoxOutput.AppendText(String.Format("{0}^2 = {1}\r\n", i, Math.Pow(i, 2)));
    i++;
    ```
- 4. Run the application by pressing **F5**. Enter a maximum value, select the While radio button, and click the **Generate** button.

### The do Statement

A *do* statement also repeatedly executes an embedded statement until the *boolean-expression* evaluates to *false*. Unlike the *while* statement, a *do* statement is a *bottom-tested* loop, so the *embedded-statement* is executed once before the *boolean-expression* is evaluated. This means it is guaranteed to execute at least one time.

The syntax for a *do* statement is

```csharp
do
    *embedded-statement*
while (*boolean-expression*);
```

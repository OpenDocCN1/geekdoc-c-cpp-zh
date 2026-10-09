
## Language Contrast: C++—Mistakenly Using = in Place of ==

C# eliminates a coding error commonly found in C and C++. In C++, Listing 4.29 is allowed.

### LISTING 4.29: C++, But Not C#, Allows Assignment as a Condition

```csharp
if (input = 9)    // Allowed in C++, not in C#
    System.Console.WriteLine(
        "Correct, tic-tac-toe has a maximum of 9 turns.");
```

Although at first glance this code appears to check whether input equals 9, Chapter 1 showed that = represents the assignment operator, not a check for equality. The return from the assignment operator is the value assigned to the variable—in this case, 9. However, 9 is an `int`, and as such it does not qualify as a Boolean expression and is not allowed by the C# compiler. The C and C++ languages treat integers that are nonzero as **true** and integers that are zero as **false**. C#, by contrast, requires that the condition actually be of a Boolean type; integers are not allowed.

## Relational and Equality Operators

**Relational and equality operators** determine whether a value is greater than, less than, or equal to another value. Table 4.2 lists all the relational and equality operators. All are binary operators.

**TABLE 4.2: Relational and Equality Operators**

| Operator | Description               | Example     |
| :------- | :------------------------ | :---------- |
| <        | Less than                 | input < 9;  |
| >        | Greater than              | input > 9;  |
| <=       | Less than or equal to     | input <= 9; |
| >=       | Greater than or equal to  | input >= 9; |
| ==       | Equality operator         | input == 9; |
| !=       | Inequality operator       | input != 9; |

The C# syntax for equality uses `==`, just as many other programming languages do. For example, to determine whether `input` equals 9, you use `input == 9`. The equality operator uses two equal signs to distinguish it from the assignment operator, =. The exclamation point signifies NOT in C#, so to test for inequality you use the inequality operator, !=.

Relational and equality operators always produce a bool value, as shown in Listing 4.30.

### LISTING 4.30: Assigning the Result of a Relational Operator to a bool Variable

```csharp
bool result = 70 > 7;
```

In the full tic-tac-toe program listing, you use the equality operator to determine whether a user has quit. The Boolean expression of Listing 4.31 includes an OR ( | ) logical operator, which the next section discusses in detail.

### LISTING 4.31: Using the Equality Operator in a Boolean Expression

```csharp
if (input == "" || input == "quit")
{
    System.Console.WriteLine($"Player {currentPlayer} quit!!");
    break;
}
```

## Logical Boolean Operators

The **logical operators** have Boolean operands and produce a Boolean result. Logical operators allow you to combine multiple Boolean expressions to form more complex Boolean expressions. The logical operators are \|, \|\|, &, &&, and ^, corresponding to OR, AND, and exclusive OR. The \| and & versions of OR and AND are rarely used for Boolean logic, for reasons which we discuss in this section.

### OR Operator ( | )

In Listing 4.31, if the user enters quit or presses the Enter key without typing in a value, it is assumed that she wants to exit the program. To enable two ways for the user to resign, you can use the logical OR operator, \|\|. The \|\| operator evaluates Boolean expressions and results in a true value if *either* operand is true (see Listing 4.32).

### LISTING 4.32: Using the OR Operator

```csharp
if ((hourOfTheDay > 23) || (hourOfTheDay < 0))
    System.Console.WriteLine("The time you entered is invalid.");
```

It is not necessary to evaluate both sides of an OR expression, because if either operand is true, the result is known to be true regardless of the value of the other operand. Like all operators in C#, the left operand is evaluated before the right one, so if the left portion of the expression evaluates to true, the right portion is ignored. In the example in Listing 4.32, if hourOfTheDay has the value 33, then (hourOfTheDay > 23) will evaluate to true and the OR operator will ignore the second half of the expression, short-circuiting it. Short-circuiting an expression also occurs with the Boolean AND operator. (Note that the parentheses are not necessary here; the logical operators are of higher precedence than the relational operators. However, it is clearer to the novice reader to parenthesize the subexpressions for clarity.)

### AND Operator (&&)

The Boolean AND operator, &&, evaluates to true only if both operands evaluate to true. If either operand is false, the result will be false. Listing 4.33 writes a message if the given variable is both greater than 10 and less than 24.[^4] Similarly to the OR operator, the AND operator will not always evaluate the right side of the expression. If the left operand is determined to be false, the overall result will be false regardless of the value of the right operand, so the runtime skips evaluating the right operand.

[^4]: The typical hours that programmers work each day.

### LISTING 4.33: Using the AND Operator

```csharp
if ((10 < hourOfTheDay) && (hourOfTheDay < 24))
    System.Console.WriteLine(
        "Hi-Ho, Hi-Ho, it's off to work we go.");
```

### Exclusive OR Operator (^)

The caret symbol, ^, is the exclusive OR (XOR) operator. When applied to two Boolean operands, the XOR operator returns true only if exactly one of the operands is true, as shown in Table 4.3.

**TABLE 4.3: Conditional Values for the XOR Operator**

| Left Operand | Right Operand | Result |
| :--- | :--- | :--- |
| True | True | False |
| True | False | True |
| False | True | True |
| False | False | False |

Unlike the Boolean AND and Boolean OR operators, the Boolean XOR operator does not short-circuit: It always checks both operands, because the result cannot be determined unless the values of both operands are known. Note that the XOR operator is exactly the same as the Boolean inequality operator.

### Logical Negation Operator (!)

The **logical negation operator**, or **NOT operator**, !, inverts a `bool` value. This operator is a unary operator, meaning it requires only one operand. Listing 4.34 demonstrates how it works, and Output 4.16 shows the result.

### LISTING 4.34: Using the Logical Negation Operator

```csharp
bool valid = false;
bool result = !valid;
// Displays "result = True"
System.Console.WriteLine($"result = { result }");
```

### OUTPUT 4.16

```
result = True
```

At the beginning of Listing 4.34, `valid` is set to `false`. You then use the negation operator on `valid` and assign the value to `result`.

In place of an if-else statement used to select one of two values, you can use the conditional operator. The conditional operator uses both a question mark and a colon; the general format is as follows:

```
condition ? consequence : alternative
```

The conditional operator is a ternary operator because it has three operands: condition, consequence, and alternative. (As it is the only ternary operator in C#, it is often called the ternary operator, but it is clearer to refer to it by its name than by the number of operands it takes.) Like the logical operators, the conditional operator uses a form of short-circuiting. If the condition evaluates to true, the conditional operator evaluates only consequence. If the condition evaluates to false, it evaluates only alternative. The result of the operator is the evaluated expression.

Listing 4.35 illustrates the use of the conditional operator. The full listing of this program appears in Chapter04\TicTacToe.cs of the source code.

### LISTING 4.35: Conditional Operator

```csharp
class TicTacToe
{
    static string Main()
    {
        // Initially set the currentPlayer to Player 1
        int currentPlayer = 1;

        // ...

        for (int turn = 1; turn <= 10; turn++)
        {
            // ...

            // Switch players
            currentPlayer = (currentPlayer == 2) ? 1 : 2;
        }
    }
}
```

The program swaps the current player. To do so, it checks whether the current value is 2. This is the conditional portion of the conditional expression. If the result of the condition is true, the conditional operator results in the consequence value, 1. Otherwise, it results in the alternative value, 2. Unlike an if statement, the result of the conditional operator must be assigned (or passed as a parameter); it cannot appear as an entire statement on its own.

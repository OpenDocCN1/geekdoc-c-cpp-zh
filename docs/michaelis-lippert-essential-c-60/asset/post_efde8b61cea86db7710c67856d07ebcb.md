
In summary, a scope is used to determine what thing a name refers to; a declaration space determines when two things declared with the same name conflict with each other. In Listing 3.27, declaring the local variable message inside the block statement embedded in the if statement restricts its scope to the block statement only; the local variable is “out of scope” when its name is used later on in the method. To avoid an error, you must declare the variable outside the block.

## LISTING 3.27: Variables Inaccessible outside Their Scope

```
class Program
{
    static void Main(string[] args)
    {
        int playerCount;
        System.Console.Write(
            "Enter the number of players (1 or 2):");
        playerCount = int.Parse(System.Console.ReadLine());
        if (playerCount != 1 && playerCount != 2)
        {
            string message =
                "You entered an invalid number of players.";
        }
        else
        {
            // ...
        }
        // Error: message is not in scope.
        System.Console.WriteLine(message);
    }
}
```

Output 3.15 shows the results of Listing 3.27.

## OUTPUT 3.15

```
...
...\Program.cs(18,26): error CS0103: The name 'message' does not exist in the current context
```

The declaration space in which a local variable’s name must be unique encompasses all the child code blocks textually enclosed within the block that originally declared the local. The C# compiler prevents the name of a local variable declared immediately within a method code block (or as a parameter) from being reused within a child code block. In Listing 3.27, because args and playerCount are declared within the method code block, they cannot be declared again anywhere within the method.

The name message refers to this local variable throughout the scope of the local variable—that is, the block immediately enclosing the declaration. Similarly, playerCount refers to the same variable throughout the block containing the declaration, including within both of the child blocks that are the consequence and the alternative of the if statement.

## Language Contrast: C++—Local Variable Scope

In C++, a local variable declared in a block is in scope from the point of the declaration statement through the end of the block. Thus an attempt to refer to the local variable before its declaration will fail to find the local variable because that variable is not in scope. If there is another thing with that name “in scope,” the C++ language will resolve the name to that thing, which might not be what you intended. In C#, the rule is subtly different: A local variable is in scope throughout the entire block in which it is declared, but it is illegal to refer to the local variable before its declaration. That is, the attempt to find the local variable will succeed, and the usage will then be treated as an error. This is just one of C#’s many rules that attempt to prevent errors common in C++ programs.

## Boolean Expressions

The parenthesized condition of the if statement is a Boolean expression. In Listing 3.28, the condition is highlighted.

## LISTING 3.28: Boolean Expression

```
if (input < 9)
{
    // Input is less than 9.
    System.Console.WriteLine(
        $"Tic-tac-toe has more than { input }" +
        " maximum turns.");
}
// ...
```

Boolean expressions appear within many control flow statements. Their key characteristic is that they always evaluate to true or false. For input < 9 to be allowed as a Boolean expression, it must result in a bool. The compiler disallows x = 42, for example, because this expression assigns x and results in the value that was assigned, instead of checking whether the value of the variable is 42.

> **Language Contrast: C++—Mistakenly Using = in Place of ==**
> 
> C# eliminates a coding error commonly found in C and C++. In C++, Listing 3.29 is allowed.
> 
> **LISTING 3.29: C++, But Not C#, Allows Assignment As a Condition**
> 
> ```cpp
> if (input = 9)    // Allowed in C++, not in C#.
>     System.Console.WriteLine(
>         "Correct, tic-tac-toe has a maximum of 9 turns.");
> ```
> 
> Although at first glance this code appears to check whether input equals 9, Chapter 1 showed that = represents the assignment operator, not a check for equality. The return from the assignment operator is the value assigned to the variable—in this case, 9. However, 9 is an int, and as such it does not qualify as a Boolean expression and is not allowed by the C# compiler. The C and C++ languages treat integers that are nonzero as true, and integers that are zero as false. C#, by contrast, requires that the condition actually be of a Boolean type; integers are not allowed.

## Relational and Equality Operators

Relational and equality operators determine whether a value is greater than, less than, or equal to another value. Table 3.2 lists all the relational and equality operators. All are binary operators.

The C# syntax for equality uses ==, just as many other programming languages do. For example, to determine whether input equals 9, you use input == 9. The equality operator uses two equal signs to distinguish it from the assignment operator, =. The exclamation point signifies NOT in C#, so to test for inequality you use the inequality operator, !=.

## TABLE 3.2: Relational and Equality Operators

| Operator | Description | Example |
|---|---|---|
| < | Less than | input<9; |
| > | Greater than | input>9; |
| <= | Less than or equal to | input<=9; |
| >= | Greater than or equal to | input>=9; |
| == | Equality operator | input==9; |
| != | Inequality operator | input!=9; |

Relational and equality operators always produce a bool value, as shown in Listing 3.30.

## LISTING 3.30: Assigning the Result of a Relational Operator to a bool Variable

```
bool result = 70 > 7;
```

In the tic-tac-toe program (see Appendix B), you use the equality operator to determine whether a user has quit. The Boolean expression of Listing 3.31 includes an OR (||) logical operator, which the next section discusses in detail.

## LISTING 3.31: Using the Equality Operator in a Boolean Expression

```
if (input == "" || input == "quit")
{
    System.Console.WriteLine($"Player {currentPlayer} quit!!");
    break;
}
```

## Logical Boolean Operators

The logical operators have Boolean operands and produce a Boolean result. Logical operators allow you to combine multiple Boolean expressions to form more complex Boolean expressions. The logical operators are |, ||, &, &&, and ^, corresponding to OR, AND, and exclusive OR. The | and & versions of OR and AND are rarely used for Boolean logic, for reasons which we discuss in this section.

## OR Operator (||)

In Listing 3.31, if the user enters quit or presses the Enter key without typing in a value, it is assumed that she wants to exit the program. To enable two ways for the user to resign, you can use the logical OR operator, ||. The || operator evaluates Boolean expressions and results in a true value if *either* operand is true (see Listing 3.32).

**LISTING 3.32: Using the OR Operator**

```csharp
if ((hourOfTheDay > 23) || (hourOfTheDay < 0))
    System.Console.WriteLine("The time you entered is invalid.");
```

It is not necessary to evaluate both sides of an OR expression, because if either operand is true, the result is known to be true regardless of the value of the other operand. Like all operators in C#, the left operand is evaluated before the right one, so if the left portion of the expression evaluates to true, the right portion is ignored. In the example in Listing 3.32, if hourOfTheDay has the value 33, then (hourOfTheDay > 23) will evaluate to true and the OR operator will ignore the second half of the expression, *short-circuiting* it. Short-circuiting an expression also occurs with the Boolean AND operator. (Note that the parentheses are not necessary here; the logical operators are of higher precedence than the relational operators. However, it is clearer to the novice reader to parenthesize the subexpressions for clarity.)

## AND Operator (&&)

The Boolean AND operator, &&, evaluates to true only if both operands evaluate to true. If either operand is false, the result will be false. Listing 3.33 writes a message if the given variable is both greater than 10 and less than 24.⁴ Similarly to the OR operator, the AND operator will not always evaluate the right side of the expression. If the left operand is determined to be false, the overall result will be false regardless of the value of the right operand, so the runtime skips evaluating the right operand.

**LISTING 3.33: Using the AND Operator**

```csharp
if ((10 < hourOfTheDay) && (hourOfTheDay < 24))
    System.Console.WriteLine(
    "Hi-Ho, Hi-Ho, it's off to work we go.");
```

4. The typical hours that programmers work each day.

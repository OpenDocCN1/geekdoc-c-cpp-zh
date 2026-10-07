```
// Displays "result = True"
Console.WriteLine("$result = { result }");
```

# OUTPUT 4.16

```
result = True
```

At the beginning of Listing 4.35, valid is set to false. You then use the negation operator on valid and assign the value to result.

# Conditional Operator (?:)

As an alternative to using an if-else statement to select one of two values, you can use the conditional operator. The conditional operator uses both question mark and colon:; the general format is as follows:

```
condition ? consequent : alternative
```

The conditional operator is a ternary operator because it has three operands: condition, consequent, and alternative. (As it is the only ternary operator in C#, it is often called the ternary operator, but it is clearer to refer to it by its name than the number of operands it takes.) Like the logical operators, the conditional operator uses a form of short-circuiting. If the conditional operator evaluates to true, the conditional operator evaluates only consequent. If the conditional operator evaluates to false, it evaluates only alternative. The result of the operator is the evaluated expression.

Listing 4.36 illustrates the use of the conditional operator. The full listing of this program appears in the source code.

# LISTING 4.36: Conditional Operator

```
public class TicTacToe
{
    public static void Main()
    {
        // Initially set the currentPlayer to Player 1
        int currentPlayer = 1;

        // ...
    }
}
```
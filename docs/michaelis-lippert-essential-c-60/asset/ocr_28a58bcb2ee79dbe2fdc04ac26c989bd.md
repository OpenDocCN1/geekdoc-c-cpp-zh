# if Statement

The if statement is one of the most common statements in C#. It evaluates a **Boolean expression** (an expression that results in either true or false) called the **condition**. If the condition is true, the **consequence statement** is executed. An if statement may optionally have an else clause that contains an **alternative statement** to be executed if the condition is false. The general form is as follows:

```
if (condition)
    consequence-statement
else
    alternative-statement
```

```
```csharp
class TicTacToe     // Declares the TicTacToe class.
{
    static void Main() // Declares the entry point of the program.
    {
        string input;

        // Prompt the user to select a 1- or 2-player game.
        System.Console.Write(
            "1 - Play against the computer\n" +
            "2 - Play against another player.\n" +
            "Choose:"
        );
        input = System.Console.ReadLine();

        if(input == "1")
            // The user selected to play the computer.
            System.Console.WriteLine(
                "Play against computer selected.");
        else
            // Default to 2 players (even if user didn't enter 2).
            System.Console.WriteLine(
                "Play against another player.");
    }
}
```
```

In Listing 3.20, if the user enters 1, the program displays "Play against computer selected." Otherwise, it displays "Play against another player."
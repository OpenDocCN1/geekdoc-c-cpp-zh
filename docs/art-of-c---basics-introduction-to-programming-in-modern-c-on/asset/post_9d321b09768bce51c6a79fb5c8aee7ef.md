
```csharp
while (true) {
    var input = Console.ReadLine();
    if (ushort.TryParse(input, out ushort number) &&
        IsValidMegaNumber(number)) {
        mega = number;
        break;
    } else {
        Console.WriteLine("Input a number in the range from 1 to 25.");
        continue;
    }
}

return mega;
}

private static bool IsValidNumber(ushort num) => (num >= 1) &&
    (num <= 70);
private static bool IsValidMegaNumber(ushort num) => (num >= 1) &&
    (num <= 25);
}
```

The lottery game logic is included in the Game static class:

*mega-millions/Game.cs*

```csharp
namespace Mega;

public static class Game {
    internal const int NumWhiteBalls = 5;

    private static readonly Random rand;

    static Game() => rand = new Random();

    public static (ushort[], ushort) DrawBalls() {
        var whites = new ushort[NumWhiteBalls];
        for (var i = 0; i < NumWhiteBalls; i++) {
            whites[i] = (ushort)(rand.Next(75) + 1);
        }
        var gold = (ushort)(rand.Next(25) + 1);

        Array.Sort(whites);
        return (whites, gold);
    }

    public static Prize DeterminePrize(
        ushort[] whites,
        ushort gold,
        ushort[] numbers,
        ushort mega
    ) => (whites.Count(numbers.Contains), gold == mega) switch {
        (0, true) => Prize.Mega,
        (1, true) => Prize.OnePlusMega,
        (2, true) => Prize.TwoPlusMega,
        (3, false) => Prize.Three,
        (3, true) => Prize.ThreePlusMega,
        (4, false) => Prize.Four,
        (4, true) => Prize.FourPlusMega,
        (5, false) => Prize.Five,
        (5, true) => Prize.Jackpot,
        _ => Prize.None,
    };
}
```

Finally, the file, *Prize.cs*, includes the definition of an "enum type", *Prize*:

*mega-millions/Prize.cs*

```csharp
namespace Mega;
{
public enum Prize : byte {
None = 0,
Mega,
OnePlusMega,
TwoPlusMega,
Three,
ThreePlusMega,
Four,
FourPlusMega,
Five,
Jackpot, // Five + Mega
}
}
```

## 15.2. Code Reading - Lottery Simulation

Try to read and understand the program even if you do not know the rules of the game, Mega Millions.

"Reading" is generally more difficult than "writing". If you are new to programming, then the (long) code samples like this can be intimidating. *Where do I start?*

As you might have noticed, we always try to list the code samples "from top to bottom" in each lesson. It is generally the best way to "read" the code, that is, to start from the top and go down, or go "deeper". For example, the game’s high level logic is all included in the `Millions` class in this example. Even if you do not know how exactly the methods like `Game.DrawBalls()` and `Game.DeterminePrize()` are implemented, you can get the general sense of how the overall program works just by looking at the `Millions.Play()` method (which is called from our "main program").

In fact, the `Play()` static method includes four "parts":

- Reading the user input, e.g., `Input.Read()` (line 5).
- Drawing the balls, e.g., `Game.DrawBalls()` (line 8).
- Checking the user input against the drawn balls, e.g., `Game.DeterminePrize()` (line 11).
- And, finally, outputting the game result, e.g., lines 12 – 16.

Now, you can examine each of these parts in turn, possibly going through different classes, and different source files, etc. And, you go further and further down, if you need to, when you read large programs.

### 15.2.1. Explanation

As before, we just use dotnet run during the development, rather than using the commands dotnet build or dotnet publish.

The program starts by asking the player for 6 numbers, 5 for the white balls and 1 for the Mega ball.

Here's a sample run:

```text
$ dotnet run

Let's play Fake Mega Millions (for fun)!
Select 5 numbers between 1 and 70: 3 19 65 23 7 ①
Select 1 mega number between 1 and 25: 10 ②
You selected: numbers = [3,7,19,23,65]; Mega number = 10
White balls drawn = [1,21,22,45,73]; The golden ball = 17
Thanks for playing Fake Mega Millions!
```

- ① A user input of 5 numbers from 1 to 70.
- ② Another input of a number from 1 to 25.

The program prints out the text "Thanks for playing Fake Mega Millions!", gently letting the player know that he/she did not win any prize ③, and it terminates.

Here's another sample run, in which the player has won a prize:

```text
$ dotnet run

Let's play Fake Mega Millions (for fun)!
Select 5 numbers between 1 and 70: 22 33 11 66 55
Select 1 mega number between 1 and 25: 15
You selected: numbers = [11,22,33,55,66]; Mega number = 15
White balls drawn = [4,9,22,46,59]; The golden ball = 15
Congratulations! You won!!! Your prize is OnePlusMega!
```

The probability of winning any prize is pretty small. You can easily (at least approximately) compute the odds of winning a prize, and it's less than 5%. The author had to play this game many times to get the one win (so that he could include its output in the book). It was the most difficult part of writing this book. 😊

### 15.2.2. Grammar

An *enum* type is a value type. It defines a custom integral numeric type. The enum types are used essentially to define a set of (related) named integer constants.

To define an enum type, we use the *enum* keyword and specify the names of enum members:

```csharp
enum Prize {
   Mega,
   // ...
}
```

By default, the associated constant values of the enum members are of type *int*. You can explicitly specify any other integral numeric type as the underlying type of an enum type. For example,

```csharp
enum Prize : byte {
   Mega,
   // ...
}
```

The enum values start with zero by default and increase by one in the order defined. One can also explicitly set a specific constant value for each enum member, if desired.

```csharp
enum Prize : byte {
    Mini = 10,
    Mega = 100,
    Super,
    // ...
}
```

In this example, the value of `Super` is 101 following the “increase by one” rule (because it is assigned no specific value and the value of its preceding member is 100).

The default value of an enum type `E` is the value corresponding to an int value 0 (even if zero doesn’t have the corresponding enum member). It is a good practice to define a default value for an enum type (or, for any value type). In the sample code, we define `Prize.None` as the default value (0).

We cannot define a method inside the definition of an enum type. To add functionality to an enum type, we use the extension methods.

The `System.Enum` class of .NET, from which all custom enum types (implicitly) inherit, defines a number of useful methods, including the `Parse()` and `TryParse()` methods that we have seen before (in numeric types). Other commonly used methods are, `IsDefined()`, `GetName()`, `GetNames()`, and `GetValues()`. Refer to the .NET online documentation for more information, if you are interested.

A switch expression is used to evaluate a single expression from a list of candidate expressions based on the pattern match with an input expression.

For example, the `Game.DeterminePrize()` method uses a switch expression, based on an input expression, (whites.Count(numbers.Contains), gold == mega), which is a tuple literal of type (int, bool). This switch expression has nine “arms” for possible match expressions, one for each Prize, separated by commas (,), and one “catch-all” arm (_) in case none of the patterns matches.

> The wildcard catch-all pattern should be the last one. Why?

The result of a switch expression is the value of the expression of the first switch expression arm whose pattern matches the input expression and whose case guard, if present, evaluates to true. The switch expression arms are evaluated in the order specified, from beginning to end.

Even though you may not know the exact syntax of the switch expression, you can still intuitively see what is happening in this switch expression.

A "case guard" is an additional condition that must be satisfied together with a matched pattern. You specify a case guard after the when keyword that follows a pattern. Although we do not use the case guards in any of the example code in this book, they can be very useful in differentiating similar patterns based on different conditions. Refer to the C# language reference for more information.

Note that the entire definition of the method, `Game.DeterminePrize()`, is included in a single expression. (As mentioned, the `return` statement is implied in the expression body.) If you are coming from the more traditional (C-style) programming style, then it may require some getting-used-to.

It is a matter of preference, but as stated, this is the future of C#. The modern C# prefers using expressions over statements, and the more compact over the more verbose.

As for the strange-looking method call `whites.Count(numbers.Contains)`, `T[].Count()` is a LINQ method.

It is an extension method defined in the System.Linq namespace, and its function signature is something like this: `int Count<T> (this IEnumerable<T> source, Func<T, bool> predicate)`. Note that we can use this method with `whites` because the type `ushort[]` is a subtype of `IEnumerable<ushort>`.

In this example, the `whites.Count()` method is called with the argument, `numbers.Contains` (without the parentheses), as a delegate of type `Func<T,bool>`.

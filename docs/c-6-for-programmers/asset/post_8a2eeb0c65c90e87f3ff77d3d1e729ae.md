
```csharp
// enumeration with constants that represent common rolls of the dice
private enum DiceNames
{
    SnakeEyes = 2,
    Trey = 3,
    Seven = 7,
    YoLeven = 11,
    BoxCars = 12
}

// plays one game of craps
static void Main()
{
    // gameStatus can contain Continue, Won or Lost
    Status gameStatus = Status.Continue;
    int myPoint = 0; // point if no win or loss on first roll

    int sumOfDice = RollDice(); // first roll of the dice

    // determine game status and point based on first roll
    switch ((DiceNames) sumOfDice)
    {
        case DiceNames.Seven: // win with 7 on first roll
        case DiceNames.YoLeven: // win with 11 on first roll
            gameStatus = Status.Won;
            break;
        case DiceNames.SnakeEyes: // lose with 2 on first roll
        case DiceNames.Trey: // lose with 3 on first roll
        case DiceNames.BoxCars: // lose with 12 on first roll
            gameStatus = Status.Lost;
            break;
        default: // did not win or lose, so remember point
            gameStatus = Status.Continue; // game is not over
            myPoint = sumOfDice; // remember the point
            Console.WriteLine($"Point is {myPoint}");
            break;
    }

    // while game is not complete
    while (gameStatus == Status.Continue) // game not Won or Lost
    {
        sumOfDice = RollDice(); // roll dice again

        // determine game status
        if (sumOfDice == myPoint) // win by making point
        {
            gameStatus = Status.Won;
        }
        else
        {
            // lose by rolling 7 before point
            if (sumOfDice == (int) DiceNames.Seven)
            {
                gameStatus = Status.Lost;
            }
        }
    }

    // display won or lost message
    if (gameStatus == Status.Won)
    {
        Console.WriteLine("Player wins");
    }
    else
    {
        Console.WriteLine("Player loses");
    }
}

// roll dice, calculate sum and display results
static int RollDice()
{
    // pick random die values
    int die1 = randomNumbers.Next(1, 7); // first die roll
    int die2 = randomNumbers.Next(1, 7); // second die roll

    int sum = die1 + die2; // sum of die values

    // display results of this roll
    Console.WriteLine($"Player rolled {die1} + {die2} = {sum}");
    return sum; // return sum of dice
}
}
```

```text
Player rolled 2 + 5 = 7
Player wins

Player rolled 2 + 1 = 3
Player loses

Player rolled 2 + 4 = 6
Point is 6
Player rolled 3 + 1 = 4
Player rolled 5 + 5 = 10
Player rolled 6 + 1 = 7
Player loses

Player rolled 4 + 6 = 10
Point is 10
Player rolled 1 + 3 = 4
Player rolled 1 + 3 = 4
Player rolled 2 + 3 = 5
Player rolled 4 + 4 = 8
Player rolled 6 + 6 = 12
Player rolled 4 + 4 = 8
Player rolled 4 + 5 = 9
Player rolled 2 + 6 = 8
Player rolled 6 + 6 = 12
Player rolled 6 + 4 = 10
Player wins
```

## 7.9.1 Method RollDice

In the rules of the game, the player must roll two dice on the first roll and must do the same on all subsequent rolls. We declare method RollDice (lines 83–94) to roll the dice and compute and display their sum. Method RollDice is declared once, but it’s called from two places (lines 30 and 54) in method Main, which contains the logic for one complete game of craps. Method RollDice takes no arguments, so it has an empty parameter list. Each time it’s called, RollDice returns the sum of the dice as an int. Although lines 86 and 87 look the same (except for the die names), they do not necessarily produce the same result. Each of these statements produces a random value in the range 1–6. Variable randomNumbers (used in lines 86–87) is not declared in the method. Rather it’s declared as a private static variable of the class and initialized in line 8. This enables us to create one Random object that’s reused in each call to RollDice.

## 7.9.2 Method Main's Local Variables

The game is reasonably involved. The player may win or lose on the first roll or may win or lose on any subsequent roll. Method Main (lines 24–80) uses local variable gameStatus (line 27) to keep track of the overall game status, local variable myPoint (line 28) to store the “point” if the player does not win or lose on the first roll and local variable sumOfDice (line 30) to maintain the sum of the dice for the most recent roll. Variable myPoint is initialized to 0 to ensure that the app will compile. If you do not initialize myPoint, the compiler issues an error, because myPoint is not assigned a value in every case of the switch statement—thus, the app could try to use myPoint before it’s definitely assigned a value. By contrast, gameStatus does not require initialization because it’s assigned a value in every branch of the switch statement—thus, it’s guaranteed to be initialized before it’s used. However, as good practice, we initialize it anyway.

## 7.9.3 enum Type Status

Local variable gameStatus (line 27) is declared to be of a new type called Status, which we declared in line 11. Status is a user-defined type called an enumeration, which declares a set of constants represented by identifiers. An enumeration is introduced by the keyword enum and a type name (in this case, Status). As with a class, braces { and } delimit the body of an enum declaration. Inside the braces is a comma-separated list of enumeration constants—by default, the first constant has the value 0 and each subsequent constant’s value is incremented by 1. The enum constant names must be unique, but the value associated with each constant need not be. Type Status is declared as a private member of class Craps, because Status is used only in that class.

Variables of type Status should be assigned only one of the three constants declared in the enumeration. When the game is won, the app sets local variable gameStatus to Status.Won (lines 37 and 59). When the game is lost, the app sets gameStatus to Status.Lost (lines 42 and 66). Otherwise, the app sets gameStatus to Status.Continue (line 45) to indicate that the dice must be rolled again.

> **Good Programming Practice 7.2**
>
> Using enumeration constants (like Status.Won, Status.Lost and Status.Continue) rather than literal integer values (such as 0, 1 and 2) can make code easier to read and maintain.

## 7.9.4 The First Roll

Line 30 in method Main calls RollDice, which picks two random values from 1 to 6, displays the value of the first die, the value of the second die and the sum of the dice, and returns the sum of the dice. Method Main next enters the switch statement at lines 33–49, which uses the sumOfDice value to determine whether the game has been won or lost, or whether it should continue with another roll.

## 7.9.5 enum Type DiceNames

The sums of the dice that would result in a win or loss on the first roll are declared in the DiceNames enumeration in lines 14–21. These are used in the switch statement’s cases. The identifier names use casino parlance for these sums. In the DiceNames enumeration we assign a value explicitly to each identifier name. When the enum is declared, each constant in the enum declaration is a constant value of type int. If you do not assign a value to an identifier in the enum declaration, the compiler will do so. If the first enum constant is unassigned, the compiler gives it the value 0. If any other enum constant is unassigned, the compiler gives it a value one higher than that of the preceding enum constant. For example, in the Status enumeration, the compiler implicitly assigns 0 to Status.Continue, 1 to Status.Won and 2 to Status.Lost.

## 7.9.6 Underlying Type of an enum

You could also declare an enum’s underlying type to be byte, sbyte, short, ushort, int, uint, long or ulong by writing

```csharp
private enum MyEnum : typeName {Constant1, Constant2, ...}
```

## 7.9.7 Comparing Integers and enum Constants

If you need to compare a simple integral type value to the underlying value of an enumeration constant, you must use a cast operator to make the two types match—there are no implicit conversions between enum and integral types. In the switch expression (line 33),

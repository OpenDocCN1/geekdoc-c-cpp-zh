
## Chapter 7 Methods: A Deeper Look

| Face | Frequency |
| :--- | :--- |
| 1 | 10002183 |
| 2 | 9997815 |
| 3 | 9999619 |
| 4 | 10000612 |
| 5 | 9994806 |
| 6 | 9999565 |

**Fig. 7-1** | Roll a six-sided die 60,000 times. (Part of 3.)

As the two sample output shows, the values produced by next enable the app to realistically simulate rolling a six-sided die. The app used nested statements (the switch is nested inside the for) to determine the number of times each side of the die occurred. The for statement (lines 19–45) iterate 60,000 times. During each iteration, line 21 produces a random value from 1 to 6. This face value is then used as the switch expression (line 24). Based on the face value, the switch statement increments one of the counter variables during each iteration of the loop. (In Section 8.4.7, we show an elegant way to replace the entire switch statement in this app with a single statement.) The switch statement has no default label because we have a label for every possible die value that the value in line 21 can produce. Run the app several times you execute this app, it produces different results.

## 7.8.7 Scaling and Shifting Random Numbers

Previously, we demonstrated the statement

```
int face = randomNumbers.Next(1, 7);
```

which simulates the rolling of a six-sided die. This statement always assigns to variable face an integer in the range 1 ≤ face < 7. The width of the range (i.e., the number of consecutive integers in the range) is 6, and the starting number in the range is 1. Referring to the preceding statement, we see that the width of the range is determined by the difference between the two integers passed to Random method Next, and the starting number of the range is the value of the first argument. We can generalize this as

```
int number = randomNumbers.Next(shiftingValue, shiftingValue + scalingFactor);
```

where shiftingValue specifies the first number in the desired range of consecutive integers and scalingFactor specifies how many numbers are in the range.

It's also possible to choose integers at random sets of values other than consecutive integers. For this purpose, it's simpler to use the version of the Next method that takes only one argument. For example, to obtain a random value from the sequence 2, 5, 8, 11 and 14, you can use the statement

```
int number = 2 + 3 * randomNumbers.Next(5);
```

In this case, randomNumbers.Next(5) produces values in the range 0–4. Each value produced is multiplied by 3 to produce a number in the sequence 0, 3, 6, 9 and 12. We then add 2 to value to shift the range of values and obtain a value from the sequence 2, 5, 8, 11 and 14. We can generalize this result as

```
int number = shiftingValue + differenceBetweenValues.Next(scalingFactor);
```

where shiftingValue represents the first number in the desired range of values, differenceBetweenValues represents the difference between consecutive numbers in the sequence and scalingFactor how many numbers are in the range.

## 7.8.8 Repeatability for Testing and Debugging

As mentioned earlier in this section, the methods of Random actually generate pseudorandom numbers based on complex mathematical calculations. Repeating any of Random's numbers produces a sequence of numbers that appear to be random. The calculation that produces the pseudorandom uses a seed to change the sequence's starting point. Each new Random object seeds itself with a value based on the computer system's clock at the time it is created, each execution of an app to produce a different sequence of random numbers.

When debugging an app, it sometimes helps to repeat the same sequence of pseudorandom numbers during each execution of the app. This repeatability enables you to prove that your app is working for a specific sequence of random numbers before you test the app with different sequences of random numbers. When repeatability is important, you can create a Random object as:

```
Random randomNumbers = new(seedValue);
```

The seedValue argument (an int) seeds the random-number calculation—using the same seedValue every time produces the same sequence of random numbers. Different seed values, of course, produce different sequences of random numbers.

## 7.9 Case Study: A Game of Chance; Introducing Enumerations

One popular game of chance is the dice game known as "craps," which is played in casinos and back throughout the world. The rules of the game are straightforward:

- You roll two dice. Each die has six faces, containing one, two, three, four, five and six spots, respectively. After the dice have come to rest, the sum of the two faces is calculated. If the sum is 7 or 11 on the first throw, you win. If the sum is 2, 3 or 12 on the first throw (called "craps"), you lose (i.e., "the house wins). If the sum is 4, 5, 6, 8 or 9 on the first throw, that becomes your "point." To win, you must continue rolling the dice until you "point."

The app in Fig. 7.8 illustrates the game of craps, using methods (lines 24–83) to define the game. gameStatus can contain Continue, Won or Lost, respectively. The app in Fig. 7.8 illustrates the game of craps, using methods (lines 24–83) to define the game.

```csharp
// Fig. 7.8: Craps.cs
// Craps class simulates the dice.
using System;

class Craps
{
    // create random-number generator for use
    private static Random randomNumbers = new();

    // enumeration with constants
    private enum Status { Continue, Won, Lost }

    // enumeration with constants that represent dice
    private enum DiceNames
    {
        SnakeEyes = 2,
        Trey = 3,
        Seven = 7,
        Yoleven = 11,
        BoxCars = 12
    }

    // plays one game
    static void Main()
    {
        // gameStatus can contain Continue, Won or Lost
        Status gameStatus = Status.Continue; // game status
        int myPoint = 0;
        int sumOfDice = RollDice(); // first roll

        // determine game status based on first roll
        switch (DiceNames)sumOfDice
        {
            case DiceNames.Seven: // win with 7
            case DiceNames.Yoleven: // win with 11
                gameStatus = Status.Won;
                break;
            case DiceNames.SnakeEyes: // lose with 2
            case DiceNames.Trey: // lose with 3
            case DiceNames.BoxCars: // lose with 12
                gameStatus = Status.Lost;
                break;
            default: // did not win or lose, so remember point
                gameStatus = Status.Continue; // game not over
                myPoint = sumOfDice; // remember the point
                break;
        }

        // while game is not complete
        while (gameStatus == Status.Continue) // game not Won or Lost
        {
            sumOfDice = RollDice(); // roll again
            // determine game status
            if (sumOfDice == myPoint) // win by making point
                gameStatus = Status.Won;
            else
{
                // lose by rolling 7 before point
                if (sumOfDice == (int)DiceNames.Seven)
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
        // pick random dice values
        int dice1 = randomNumbers.Next(1, 7); // first dice roll
        int dice2 = randomNumbers.Next(1, 7); // second dice roll
        int sum = dice1 + dice2; // sum of dice values
        // display results of this roll
        Console.WriteLine($"Player rolled {dice1} + {dice2} = {sum}");
        return sum; // return sum of dice
    }
}
```

**Fig. 7-8** | Craps class simulates the dice game craps. (Part 1 of 3.)

## 7.9 Case Study: A Game of Chance: Introducing Enumerations

```csharp
sumOfDice = RollDice(); // roll again
// determine game status
if (sumOfDice == myPoint) // win by making point
    gameStatus = Status.Won;
else
{
    // lose by rolling 7 before point
    if (sumOfDice == (int)DiceNames.Seven)
    {
        gameStatus = Status.Lost;
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
// roll dice, calculate sum and display results
static int RollDice()
{
    // pick random dice values
    int dice1 = randomNumbers.Next(1, 7); // first dice roll
    int dice2 = randomNumbers.Next(1, 7); // second dice roll
    int sum = dice1 + dice2; // sum of dice values
    // display results of this roll
    Console.WriteLine($"Player rolled {dice1} + {dice2} = {sum}");
    return sum; // return sum of dice
}
```

**Fig. 7-8** | Craps class simulates the dice game craps. (Part 2 of 3.)


```cpp
cout << "Enter seed: ";
cin >> seed;
srand( seed ); // seed random number generator

// loop 10 times
for ( int counter = 1; counter <= 10; ++counter )
{
    // pick random number from 1 to 6 and output it
    cout << setw( 10 ) << ( 1 + rand() % 6 );

    // if counter is divisible by 5, start a new line of output
    if ( counter % 5 == 0 )
        cout << endl;
} // end for
} // end main
```

```text
Enter seed: 67
          6          1          4          6          2
          1          6          1          6          4
```

```text
Enter seed: 432
          4          6          3          1          6
          3          1          5          4          2
```

```text
Enter seed: 67
          6          1          4          6          2
          1          6          1          6          4
```

**Fig. 6.10** | Randomizing the die-rolling program. (Part 2 of 2.)

Let’s run the program several times and observe the results. Notice that the program produces a *different* sequence of random numbers each time it executes, provided that the user enters a different seed. We used the *same* seed in the first and third sample outputs, so the *same* series of 10 numbers is displayed in each of those outputs.

To randomize without having to enter a seed each time, we may use a statement like

```cpp
srand( time( 0 ) );
```

This causes the computer to read its clock to obtain the value for the seed. Function `time` (with the argument 0 as written in the preceding statement) typically returns the current time as the number of seconds since January 1, 1970, at midnight Greenwich Mean Time (GMT). This value is converted to an unsigned integer and used as the seed to the random number generator. The function prototype for `time` is in `<ctime>`.

### Generalized Scaling and Shifting of Random Numbers

Previously, we simulated the rolling of a six-sided die with the statement

```cpp
face = 1 + rand() % 6;
```

which always assigns an integer (at random) to variable `face` in the range 1 ≤ face ≤ 6. The width of this range (i.e., the number of consecutive integers in the range) is 6 and the starting number in the range is 1. Referring to the preceding statement, we see that the width of the range is determined by the number used to scale `rand` with the modulus operator (i.e., 6), and the starting number of the range is equal to the number (i.e., 1) that is added to the expression `rand % 6`. We can generalize this result as

```text
number = shiftingValue + rand() % scalingFactor;
```

where `shiftingValue` is equal to the first number in the desired range of consecutive integers and `scalingFactor` is equal to the width of the desired range of consecutive integers.

## 6.8 Case Study: Game of Chance: Introducing enum

One of the most popular games of chance is a dice game known as “craps,” which is played in casinos and back alleys worldwide. The rules of the game are straightforward:

> A player rolls two dice. Each die has six faces. These faces contain 1, 2, 3, 4, 5 and 6 spots. After the dice have come to rest, the sum of the spots on the two upward faces is calculated. If the sum is 7 or 11 on the first roll, the player wins. If the sum is 2, 3 or 12 on the first roll (called “craps”), the player loses (i.e., the “house” wins). If the sum is 4, 5, 6, 8, 9 or 10 on the first roll, then that sum becomes the player’s “point.” To win, you must continue rolling the dice until you “make your point.” The player loses by rolling a 7 before making the point.

The program in Fig. 6.11 simulates the game. In the rules, notice that the player must roll two dice on the first roll and on all subsequent rolls. We define function `rollDice` (lines 63–75) to roll the dice and compute and print their sum. The function is defined once, but called from lines 21 and 45. The function takes no arguments and returns the sum of the two dice, so empty parentheses and the return type `int` are indicated in the function prototype (line 8) and function header (line 63).

```cpp
// Fig. 6.11: fig06_11.cpp
// Craps simulation.
#include <iostream>
#include <cstdlib> // contains prototypes for functions srand and rand
#include <ctime> // contains prototype for function time
using namespace std;

int rollDice(); // rolls dice, calculates and displays sum

int main()
{
   // enumeration with constants that represent the game status
   enum Status { CONTINUE, WON, LOST }; // all caps in constants

   int myPoint; // point if no win or loss on first roll
   Status gameStatus; // can contain CONTINUE, WON or LOST

   // randomize random number generator using current time
   srand( time( 0 ) );

   int sumOfDice = rollDice(); // first roll of the dice
```

**Fig. 6.11** | Craps simulation. (Part 1 of 3.)

```cpp
// determine game status and point (if needed) based on first roll
switch ( sumOfDice )
{
    case 7: // win with 7 on first roll
    case 11: // win with 11 on first roll
        gameStatus = WON;
        break;
    case 2: // lose with 2 on first roll
    case 3: // lose with 3 on first roll
    case 12: // lose with 12 on first roll
        gameStatus = LOST;
        break;
    default: // did not win or lose, so remember point
        gameStatus = CONTINUE; // game is not over
        myPoint = sumOfDice; // remember the point
        cout << "Point is " << myPoint << endl;
        break; // end of switch
} // end switch

// while game is not complete
while ( gameStatus == CONTINUE ) // not WON or LOST
{
    sumOfDice = rollDice(); // roll dice again

    // determine game status
    if ( sumOfDice == myPoint ) // win by making point
        gameStatus = WON;
    else
        if ( sumOfDice == 7 ) // lose by rolling 7 before point
            gameStatus = LOST;
} // end while

// display won or lost message
if ( gameStatus == WON )
    cout << "Player wins" << endl;
else
    cout << "Player loses" << endl;
} // end main

// roll dice, calculate sum and display results
int rollDice()
{
    // pick random die values
    int die1 = 1 + rand() % 6; // first die roll
    int die2 = 1 + rand() % 6; // second die roll

    int sum = die1 + die2; // compute sum of die values

    // display results of this roll
    cout << "Player rolled " << die1 << " + " << die2
         << " = " << sum << endl;
    return sum; // end function rollDice
} // end function rollDice
```

**Fig. 6.11** | Craps simulation. (Part 2 of 3.)

```text
Player rolled 2 + 5 = 7
Player wins
```

```text
Player rolled 6 + 6 = 12
Player loses
```

```text
Player rolled 1 + 3 = 4
Point is 4
Player rolled 4 + 6 = 10
Player rolled 2 + 4 = 6
Player rolled 6 + 4 = 10
Player rolled 2 + 3 = 5
Player rolled 2 + 4 = 6
Player rolled 1 + 1 = 2
Player rolled 4 + 4 = 8
Player rolled 4 + 3 = 7
Player loses
```

```text
Player rolled 3 + 3 = 6
Point is 6
Player rolled 5 + 3 = 8
Player rolled 4 + 5 = 9
Player rolled 2 + 1 = 3
Player rolled 1 + 5 = 6
Player wins
```

**Fig. 6.11** | Craps simulation. (Part 3 of 3.)

The game is reasonably involved. The player may win or lose on the first roll or on any subsequent roll. The program uses variable `gameStatus` to keep track of this. Variable `gameStatus` is declared to be of new type `Status`. Line 13 declares a user-defined type called an enumeration. An enumeration, introduced by the keyword `enum` and followed by a type name (in this case, `Status`), is a set of integer constants represented by identifiers. The values of these enumeration constants start at 0, unless specified otherwise, and increment by 1. In the preceding enumeration, the constant `CONTINUE` has the value 0, `WON` has the value 1 and `LOST` has the value 2. The identifiers in an enum must be unique, but separate enumeration constants can have the same integer value.

![](img/bfd978e7e9b192bab46ec2a89e481263_247_0.png)

> **Good Programming Practice 6.1**
>
> *Capitalize the first letter of an identifier used as a user-defined type name.*

![](img/bfd978e7e9b192bab46ec2a89e481263_247_1.png)

> **Good Programming Practice 6.2**
>
> *Use only uppercase letters in enumeration constant names. This makes these constants stand out in a program and reminds you that enumeration constants are not variables.*

Variables of user-defined type `Status` can be assigned only one of the three values declared in the enumeration. When the game is won, the program sets variable `gameStatus` to `WON` (lines 28 and 49). When the game is lost, the program sets variable

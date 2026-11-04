```
```
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
```

Fig. 7.7 | Craps class simulates the dice game craps. (Part 4 of 4.)

# 7.9.1 Method RollDice

In the rules of the game, the player must roll two dice on the first roll and must do the same on all subsequent rolls. We declare method RollDice (lines 83–94) to roll the dice and compute and display their sum. Method RollDice is declared once, but it’s called from two places (lines 30 and 54) in method Main, which contains the logic for one complete game of craps. Method RollDice takes no arguments, so it has an empty parameter list. Each time it’s called, RollDice returns the sum of the dice as an int. Although lines 86 and 87 look the same (except for the die names), they do not necessarily produce the same result. Each of these statements produces a random value in the range 1–6. Variable randomNumbers (used in lines 86–87) is not declared in the method. Rather it’s declared as a private static variable of the class and initialized in line 8. This enables us to create one Random object that’s reused in each call to RollDice.

# 7.9.2 Method Main's Local Variables

The game is reasonably involved. The player may win or lose on the first roll or may win or lose on any subsequent roll. Method Main (lines 24–80) uses local variable gameStatus (line 27) to keep track of the overall game status, local variable myPoint (line 28) to store the “point” if the player does not win or lose on the first roll and local variable sumOfDice (line 30) to maintain the sum of the dice for the most recent roll. Variable myPoint is initialized to 0 to ensure that the app will compile. If you do not initialize myPoint, the compiler issues an error, because myPoint is not assigned a value in every case of the switch statement—thus, the app could try to use myPoint before it’s definitely assigned a value. By contrast, gameStatus does not require initialization because it’s assigned a value in every branch of the switch statement—thus, it’s guaranteed to be initialized before it’s used. However, as good practice, we initialize it anyway.

# 7.9.3 enum Type Status

Local variable gameStatus (line 27) is declared to be of a new type called Status, which we declared in line 11. Status is a user-defined type called an enumeration, which declares a set of constants represented by identifiers. An enumeration is introduced by the keyword enum and a type name (in this case, Status). As with a class, braces { and } delimit the
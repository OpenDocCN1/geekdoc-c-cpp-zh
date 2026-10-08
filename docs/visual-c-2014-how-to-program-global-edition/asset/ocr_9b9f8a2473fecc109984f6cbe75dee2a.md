# 7.9 Case Study: A Game of Chance: Introducing Enumerations

```
sumOfDice = RollDice(); // roll dice again
// determine game status
if (sumOfDice == myPoint) // win by making point
    gameStatus = Status.Won;
else {
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
}\else {
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
    Console.WriteLine("Player rolled {dice1} + {dice2} = {sum}");
    return sum; // return sum of dice
}
```

![](bbox=[0.125, 0.775, 0.87, 0.832])

![](bbox=[0.125, 0.872, 0.87, 0.928])

Fig. 7.8 | Craps class simulates the dice game craps. (Part 2 of 3.)
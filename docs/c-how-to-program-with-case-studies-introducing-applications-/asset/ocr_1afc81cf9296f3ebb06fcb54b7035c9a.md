```
// display won or lost message
if (WON == gameStatus) { // did player win?
    puts("Player wins");
} else { // player lost
    puts("Player loses");
}
}

// roll dice, calculate sum and display results
int rollDice(void) {
    int die1 = 1 + (rand() % 6); // pick random die1 value
    int die2 = 1 + (rand() % 6); // pick random die2 value

    // display results of this roll
    printf("Player rolled %d + %d = %d\n", die1, die2, die1 + die2);
    return die1 + die2; // return sum of dice
}
```

# Player wins on the first roll:

```
Player rolled 5 + 6 = 11
Player wins
```

# Player wins on a subsequent roll:

```
Player rolled 4 + 1 = 5
Point is 5
Player rolled 6 + 2 = 8
Player rolled 2 + 1 = 3
Player rolled 3 + 2 = 5
Player wins
```

# Player loses on the first roll:

```
Player rolled 1 + 1 = 2
Player loses
```

# Player loses on a subsequent roll:

```
Player rolled 6 + 4 = 10
Point is 10
Player rolled 3 + 4 = 7
Player loses
```

# Fig. 5.7 | Simulating the game of craps. (Part 2 of 2.)

In the game, the player must roll two dice on each roll. We define the rollDice function to roll the dice and compute and print their sum. The function is defined once, but it’s called twice (lines 16 and 41). The function takes no arguments, so we’ve indicated void in the parameter list (line 62) and the function prototype (line 9). Function rollDice does return the sum of the two dice, so a return type of int is indicated in its function header and in its function prototype.
```
```csharp
63        // lose by rolling 7 before point
64        if (sumOfDice == (int) DiceNames.Seven)
65        {
66            gameStatus = Status.Lost;
67        }
68
69    }
70
71    // display won or lost message
72    if (gameStatus == Status.Won)
73    {
74        Console.WriteLine("Player wins");
75    }
76    else
77    {
78        Console.WriteLine("Player loses");
79    }
80    }
81
82    // roll dice, calculate sum and display results
83    static int RollDice()
84    {
85        // pick random die values
86        int die1 = randomNumbers.Next(1, 7); // first die roll
87        int die2 = randomNumbers.Next(1, 7); // second die roll
88
89        int sum = die1 + die2; // sum of die values
90
91        // display results of this roll
92        Console.WriteLine($"Player rolled {die1} + {die2} = {sum}");
93        return sum; // return sum of dice
94    }
95    }
```
```

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

Fig. 7.7 | Craps class simulates the dice game craps. (Part 3 of 4.)
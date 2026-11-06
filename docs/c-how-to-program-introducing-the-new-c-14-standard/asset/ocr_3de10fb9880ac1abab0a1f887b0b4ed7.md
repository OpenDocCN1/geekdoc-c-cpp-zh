```
BANG !!!!!
AND THEY'RE OFF !!!!!
```

For each tick of the clock (i.e., each iteration of a loop), display a 70-position line showing the letter `T` in the tortoise’s position and the letter `H` in the hare’s position. Occasionally, the contenders land on the same square. In this case, the tortoise bites the hare and your program should display `OUCH!!!` beginning at that position. All positions other than the `T`, the `H` or the `OUCH!!!` (in case of a tie) should be blank.

After displaying each line, test whether either animal has reached or passed square 70. If so, display the winner and terminate the simulation. If the tortoise wins, display `TORTOISE WINS!!! YAY!!!` If the hare wins, display `Hare wins. Yuch.` If both animals win on the same clock tick, you may want to favor the tortoise (the “underdog”), or you may want to display `It’s a tie.` If neither animal wins, perform the loop again to simulate the next tick of the clock.

+   7. 8.13 (*What Does This Code Do?*) What does this program do?
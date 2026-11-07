# ### Checkpoint

+   1. *(True/False)* When debugging a simulation, you should ensure that each time you run the program, it generates a different sequence of random numbers.
+      **Answer:** False. Actually, when debugging a simulation, random-number repeatability is essential for proving that corrections to the program work properly.
+   2. *(Code)* Rewrite the following distribution used with die rolling so that it produces two int values that could be used in a coin-tossing application to represent “heads” or “tails” with equal likelihood. Use a more appropriate `uniform_int_distribution` object name:
+      `uniform_int_distribution randomDie{1, 6};`
+      **Answer:** `uniform_int_distribution randomCoin{0, 1};`

# ### 5.9 Case Study: Game of Chance; Introducing Scoped enums

One of the most popular games of chance is a dice game known as “craps,” which is played in casinos and back alleys worldwide. The rules of the game are straightforward:

> > A player rolls two dice. Each die has six faces containing 1, 2, 3, 4, 5 and 6 spots. After the dice have come to rest, the sum of the spots on the two upward faces is calculated. If the sum is 7 or 11 on the first roll, the player wins. If the sum is 2, 3 or 12 on the first roll (called “craps”), the player loses (i.e., the “house” wins). If the sum is 4, 5, 6, 8, 9 or 10 on the first roll, then that sum becomes the player’s “point.” To win, you must keep rolling the dice until you “make your point.” The player loses by rolling a 7 before making the point.

In the rules, notice that the player must roll two dice on the first and subsequent rolls. We will define a `rollDice` function to roll the dice and compute and display their sum. The function may be called multiple times—once for the game’s first roll and possibly many more times if the player does not win or lose on the first roll. Below are the outputs of several sample executions showing:

+   - winning on the first roll by rolling a 7,
+   - winning on a subsequent roll by “making the point” before rolling a 7,
+   - losing on the first roll by rolling a 12, and
+   - losing on a subsequent roll by rolling a 7 before “making the point.”

```
~~~
Player rolled 2 + 5 = 7
Player wins
~~~
```

```
~~~
Player rolled 3 + 3 = 6
Point is 6
Player rolled 5 + 3 = 8
Player rolled 4 + 5 = 9
Player rolled 2 + 1 = 3
Player rolled 1 + 5 = 6
Player wins
~~~
```
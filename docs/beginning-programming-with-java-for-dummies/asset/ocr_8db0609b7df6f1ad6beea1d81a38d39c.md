The computer performs an iteration of the loop. During this iteration, the computer gets new values for die1 and die2 and prints those values on the screen. In the first run of Figure 12-1, the new values are 3 and 1.

The computer returns to the top of the while statement and checks to see if die1 + die2 != 7 && die1 + die2 != 11 is still true. The condition is true, so the computer takes the true path in Figure 12-3.

The computer performs another iteration of the loop. During this iteration, the computer gets new values for die1 and die2 and prints those values on the screen. In Figure 12-1, the new values are 4 and 3.

# Figure 12-2:
Two wrongs don't make a right, but two trues make a true.

![](bbox=[0.28, 0.38, 0.92, 0.62])

# Figure 12-3:
Paths through the code in Listing 12-1.

![](bbox=[0.27, 0.62, 0.92, 0.92])

```
int die1 = 0, die2 = 0;

¿ die1 + die2 != 7 && die1 + die2 != 11 ?

true

die1 = myRandom.nextInt(6) + 1;
die2 = myRandom.nextInt(6) + 1;

out.print(die1);
out.print(" ");
out.println(die2);

false

out.print("Rolled ");
out.println(die1 + die2);
```
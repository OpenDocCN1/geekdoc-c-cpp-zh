Suppose $D_{AB}$ and $D_{BA}$ are the delays for sending a message from A to B and B to A, respectively, and consider the algorithm it uses to calculate the clock error:

```
$T_{BI} = (T_{A1} + E) + D_{AB}$
$T_{A2} = (T_{BI} + E) + D_{BA}$
```

Now, if you subtract the second equation from the first, you get this:

```
$T_{BI} - T_{A2} = (T_{A1} + E + D_{AB}) - (T_{BI} + E + D_{BA})$
$= T_{A1} - T_{BI} + D_{BA} - 2 \times E$
```

In the previous analysis $D_{AB} = D_{BA}$, those two terms cancel. If you leave the terms in the equation and solve for $E$, you get this:

```
$E = (2 \times T_{BI} - T_{A2}) \div 2 = (D_{BA} - D_{AB}) \div 2$
```

The error in D due to the difference between $D_{BA}$ and $D_{AB}$ is half of their difference. In the worst case, where one of them is 0 and the other is close to the total roundtrip delay $D$, the error is $D / 2$.

After running the clock algorithm, $T_A = T_{BI} \pm 2$.

+   14. There is nearly any difference between the network's changing and it taking a different amount of time for a message to go from A to B or B to A. In either case, all matters is that the values $D_{BA}$ and $D_{AB}$ from Exercise 13 are. Answer that after the clock algorithm runs, $T_B = T_A \pm 2$, where $D$ is the total delay.
15. The answer to Exercise 14 shows that the error in process B's new time is determined by the total roundtrip delay $D$. If the network's speeds vary widely, sometimes $D$ will be short, and sometimes $D$ will be long. To get a better result, perform the algorithm several times, and adjust the time according to the trial with the smallest value for $D$.

# Chapter 19: Interview Puzzles

+   1. If he brings three socks into the living room, they can't all be different colors, so at least two will be brown or black.

This problem is simple if you have a similar problem before, so it doesn't really test the reasoning of anyone who has seen something similar. Also easy if you write down some possible combinations. Overall it's not too bad a question, but it doesn't really tell the interviewer.

+   2. If you put all the marbles in one bowl, or half of each color in one bowl, you have a 50% chance of picking a white marble, so that's a quicker lower bound for the possible probability. Similarly if you put out all of the white marbles in one bowl and all of the black marbles in the other bowl, you have a 50% chance of picking a white marble.
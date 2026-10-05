In other words, it launches a process that keeps checking the condition in the first set of brackets to see if it is true. When it is true, it runs the instruction inside the second set of brackets.

What's the difference between when and waituntil? Both when and waituntil keep checking the condition to see if it is true. When it is true, the waituntil procedure simply lets it pass to the next lines of code. It is like waituntil is a traffic cop, holding up traffic till the light green. When it turns green, the traffic moves.

When, on the other hand, checks for the green light and then lets the traffic do exactly one thing or one of lists. This might be a little nearer for us, with our multiple turtles.

We need to use when and some procedures we make may cause the user to win or lose, depending on whether they meet the winning condition (t1 touches t2), or the losing condition (t1 touches a red line).

For losing, we will make a lose procedure, which uses the reset procedure we already made. When the condition is true (t1) is touching a red line, the computer will run lose. Lose will announce "You lose!" and then will call reset.

For winning, we will use the procedure we already made. In win, t1 turns into a cloud and then into something else, waits a bit, and announces "You win! Then it calls reset.

![](bbox=[0.058, 0.403, 0.942, 0.693])

What do you think of the diagram above? Notice that it has four decision-checkers working at once, represented by a diagram. All are talking to t1, because they follow the command to talkto t1 at the beginning. Each leads to an end to the game. It represents our program?

I see two problems with it:

+   Where do we use t3 and t4? They need to be moving back and forth, 180 degrees when we use colorunder = 15. Let's put them at the beginning. Our launched movements run at the same time, so we will put them alongside each other.
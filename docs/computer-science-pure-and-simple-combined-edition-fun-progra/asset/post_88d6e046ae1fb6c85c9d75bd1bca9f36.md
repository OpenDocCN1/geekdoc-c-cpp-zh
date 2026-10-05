
Hints for Main: First, create a variable called **preference** to use within **Main**, using **local**. If you can't remember how to use **local**, look it up in the Help vocabulary (see page 15). You will also need to use **announce**, **question**, and **ifelse**. Look those up too, to jog your memory. If the user answers B for boy, you will need to make the value in the variable preference match the shape number for girl. Otherwise, you need to make the value match the shape number for girl girl. If you have MicroWorlds EX, be sure to download shapes to your shape center to use for a boy and a girl.

Hints for win: Change **win** so that it takes a variable passed to it. **Setsh** will use the value in this variable to set the shape for **t1**. So, when you call **win**, the shape will become a boy or a girl depending on what value is stored in the variable.

## #22 Maze III

### Assignment
- Add to your Mymaze maze (not the prince/princess maze) at least two moving obstacles. These will be turtles wearing shapes. They could be a fireball (sun) or a spider that you create. We will call them spiders. In your code, make a spider turn 180 degrees every time it hits a maze wall.
- When the t1 turtle bumps into a spider, the game announces “You lose”. Then it resets: the turtle goes back to the start with its head up, the same result as t1 hits a maze line.
- Put instructions for the user in a text box, something like “Use arrow keys to direct turtle.”

Let's work on the first requirement: add two moving obstacles. The obstacles turn 180 degrees every time they hit a maze wall.

First need to draw your spider, double click on one of the empty spots in the Shape Center and then use the drawing tools to make and name your spider shape. Or use a sun or some other ready-made shape. “Hatch” two more turtles (t3 and t4). Go to the Shape Center, click on the shape, and then click on the turtle. This puts the new "clothes" on the turtle so it looks like that shape. Move the turtles around by dragging them with the pointer. Put them at likely spots in your maze.

You will have separate sections of code addressed to each turtle: t1, t3, and t4 (t2 is your destination castle and won't be moving). Here is some pseudocode for example:

```
:talk to t1
:launch a movement for t1
:end that movement under a certain condition.
```

For the ending movement, we first used waituntil. But when we are talking to multiple turtles all launched into various movements, waituntil doesn't work well. There is a similar built-in procedure that we can use. That is when.

To jog your memory, look up in the Help vocabulary:

when true-or-false-instruction-list instruction-list
Starts a parallel process that repeatedly tests whether the first instruction list reports true or false. If it reports true, the second instruction list is run. To stop a when, use cancel on the true-or-false-instruction-list, the Cancel menu item, the Stop All menu item, or press Ctrl+Break.

Example:
when (ycor > 50)[bk 20]

In other words, it launches a process that keeps checking the condition in the first set of brackets to see if it is true. When it is true, it runs the instruction inside the second set of brackets.

What's the difference between when and waituntil? Both when and waituntil keep checking the condition to see if it is true. When it is true, the waituntil procedure simply lets it pass to the next lines of code. It is like waituntil is a traffic cop, holding up traffic till the light green. When it turns green, the traffic moves.

When, on the other hand, checks for the green light and then lets the traffic do exactly one thing or one of lists. This might be a little nearer for us, with our multiple turtles.

We need to use when and some procedures we make may cause the user to win or lose, depending on whether they meet the winning condition (t1 touches t2), or the losing condition (t1 touches a red line).

For losing, we will make a lose procedure, which uses the reset procedure we already made. When the condition is true (t1) is touching a red line, the computer will run lose. Lose will announce "You lose!" and then will call reset.

For winning, we will use the procedure we already made. In win, t1 turns into a cloud and then into something else, waits a bit, and announces "You win! Then it calls reset.

![](img/242aaa06c3a3208f16d97cdd92303648_136_0.png)

What do you think of the diagram above? Notice that it has four decision-checkers working at once, represented by a diagram. All are talking to t1, because they follow the command to talkto t1 at the beginning. Each leads to an end to the game. It represents our program?

I see two problems with it:

- Where do we use t3 and t4? They need to be moving back and forth, 180 degrees when we use colorunder = 15. Let's put them at the beginning. Our launched movements run at the same time, so we will put them alongside each other.

2. For the colorer check we could use when instead of waituntil, now that we changed what happens after waituntil. Instead of several commands, now it is just one procedure. Using the same commands (when) everywhere would be a little neater, wouldn't it?

Take look at this diagram. Will it do?

![](img/242aaa06c3a3208f16d97cdd92303648_137_0.png)

I want you to write some pseudocode in Main to match this diagram. DO NOT TURN PAGE until you have a draft. It doesn't have to be perfect! Just work on it for a little, get it into your head.

Here is my pseudocode:

```
to Main
talk to t1
launch forward movement, and turn using arrow keys

talkto t3
launch forward movement
when t3 touches red, turn 180 degrees

talkto t4
launch forward movement
when t4 touches red, turn 180 degrees

talkto t1
when t1 touches red, lose (a separate procedure)
when t1 touches t2, win (a separate procedure)
when t1 touches t3, lose (a separate procedure)
when t1 touches t4, lose (a separate procedure)
```

### Code

Let's recall our Mymaze code from the last lesson:

```
to Main
talk "t1"
launch [repeat 2000 [forward move]]
when [touching] "t1" "t2" [win]
waituntil [colorunder = 15]
announce [You lose!]
reset
```

```
to key
if key = 28 [seth 270 fd 1]
if key = 29 [seth 90 fd 1]
if key = 30 [seth 0 fd 1]
if key = 31 [seth 180 fd 1]
if key = 37 [seth 270 fd 1]
if key = 39 [seth 90 fd 1]
if key = 38 [seth 0 fd 1]
if key = 40 [seth 180 fd 1]
if key = "s" [stopall]
```

to go
Main
end

to win
announce [You win!]
talkto "t1"
set wait 2
setsh random 60 wait 10
reset

to reset
talkto "t1"
setpos [-319 -164]
seth 0
setsh 0
end

First of all, let's add a procedure, to lose. It will announce “You lose!” and call reset. Go ahead and code that one.

Now, let's look at Main. We're going to start with our new pseudocode and rewrite Main. First we'll take the new pseudocode and plug in useful lines of code from the previous Mymaze.

to Main
talkto t1
talk "t1"
launch forward movement, and turn using arrow keys
launch [repeat 2000 [forward move]]

Can you come up with code for the next two lines of pseudocode, talking to t3? Our forward movement will use launch, repeat, and forward. Use a large number for the repeat.

talkto t3
launch forward movement

Now, code the next line, using when, colorunder, and right:
when t3 touches red, turn 180 degrees

Now, code the next three lines, using the previous three as a model:
talkto t4
launch forward movement
when t4 touches red, turn 180 degrees

Now, code the next line. You will need to talkto "t1" again. Then you will need "when" and colorunder.

when t1 touches red, lose (a separate procedure)

The next line is already done for us, from the previous Mymaze:
when t1 touches t2, win (a separate procedure)
when [touching] "t1" "t2" [win]

Now, code the last two lines, using the one above as a model.
when t1 touches t3, lose (a separate procedure)
when t1 touches t4, lose (a separate procedure)

You’ll need to delete the pseudocode lines once you get the thing working. Be sure your maze lines are thick; otherwise the spiders may not see them.

Remember this part of the assignment?

- Put instructions for the user in a text box that shows a box filled with "A" or "ABC".

Make a text box (using the icon that shows a box filled with “A” or “ABC”). Put in some instructions for the user. Move the box to a good spot by holding down the left mouse button and dragging the box around.

Now, pull it all together and run the maze with the spiders! Save it as Mymaze.

## Extra Credit

Use a slider (a picture of a button that slides) to let the user adjust the speed of the sun/spider. Hatch a slider in MicroWorlds EX using this icon The new slider will be called slider1. Use this name instead of a number input, for instance forward slider1. It will need to be in the code that launches the movements for the spiders. t3 and t4. Now, adjust the slider and play around with it. Save this as slidermaze, and don’t use it for the next lesson!

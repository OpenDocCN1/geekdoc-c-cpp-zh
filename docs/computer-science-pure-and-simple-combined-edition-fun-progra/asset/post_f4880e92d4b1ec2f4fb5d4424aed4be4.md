
## #30 Hangman IV

Here’s our next requirement:
Make a six-piece drawing that adds a piece of a hanging man each time the user makes a wrong guess. Use hidden turtles for each piece of the man (**ht** is a command that hides a turtle); **st** is a command that shows a hidden turtle.)

First, go to the shape center and make six shapes that will make up a hanging man. You can name them like this: noose, head, body, arm1, arm2, legs.

Now, on your Page 1, use the drawing tools to draw a bar that the noose will hang from. Hatch five more turtles. Put the shapes on them in order: noose on **t1**, head on **t2**, body on **t3**, and so on. Drag them around so that they make a drawing of a hanging man. Change the part drawings if you need to make them up. Be sure to put the hanging man drawing off to the side of the page, where it won’t be covered by the question/announcement box in the middle.

![](img/242aaa06c3a3208f16d97cdd92303648_172_0.png)

From Hannah’s Hangman: Hanging in Progress

What we want to do is at the beginning hide the turtles that make up the drawing, and show them one by one as the counter number increases. You can think of a way to do that? Think about it before you turn the page. Use **ht** to hide a turtle and st to show a turtle.

Here's what we can do: At the beginning of the code, just after the list of variables, talk to the list of all the turtles, and then command ht for hide turtle.

Lower down in the program, inside the loop near the end, we will make a set of if statements, meaning:

```
if the counter equals 1, talk to t1, show the turtle, and set its shape to noose.
```

Can you translate that to Logo? And make more for the rest of the body parts?

## Exercises

- 1. Make another shape that shows the hanging man is a goner (eyes are x's for instance). Change to that shape after the computer announces “You lose!”

- 2. Make a separate procedure called win. In the winning case, hide all but one of the turtles. For the one still showing, change the shape to something fun, like a fireball. Animate it.

![](img/242aaa06c3a3208f16d97cdd92303648_173_0.png)

Hannah’s Hangman Is a Goner!

## #31 City I

This is a game that asks the user for directions and then draws a busy street, lined with houses and full of animated characters zipping back and forth. Or it could be a variation on this; one student drew an army camp of barracks with jeeps, trucks, and airplanes moving through and above it, complete with blinking lights. Use your imagination when you plan your city! Here are two examples:

![](img/242aaa06c3a3208f16d97cdd92303648_174_0.png)

My City

![](img/242aaa06c3a3208f16d97cdd92303648_174_1.png)

Paul’s Army Camp

Here is the plan:

- The user presses the Start button.
- The drawing turtle moves to the left edge of the screen, near the bottom so the question boxes won't cover up the house it draws.
- The computer says to you, "I will build you a house. Do you want big or small? (type big or small)"
- The turtle, tl, draws a house, sized big or small. The houses are identical except for size.
- It waits a bit so the user can see the drawing.
- The computer asks, “Do you want 1 or 2 windows?”
- T1 draws one or two windows. It waits a bit.
- The computer asks, “Do you want a red or blue house?”
- T1 colors the house in red or blue (or two other colors you choose). Now the house is built. It moves to the right steps.
- The computer asks, “Do you want another house? Y or N”
- If the user answers “Y,” the loop starts over. We could end up with a street lined with houses.
- After the city is drawn, the program launches at least three animations walking or flying down the street (across the screen).
- The user can stop the animations and start over by pressing Start.

There are two things about this program I want to notice right off the bat. One is that it contains a loop. It repeats a set of steps over and over. The other is that it uses variables. The house procedure will use a variable sent from Main to determine what size to draw the house.

I want you to take out a pencil and paper and work on a flow chart for this program. Don't turn the to look at mine until you have worked on it for 10 minutes. Hint: it looks a lot like the one for Race, but there is a loop in it.

![](img/242aaa06c3a3208f16d97cdd92303648_177_0.png)

## Flow Chart for City

First, let's consider what code we will use to make our loop. We will have a bunch of steps, and at the end of the steps, we will get input from the user on whether to loop or not. We could pattern our loop after Hangman loop, using forever to start it, and stopping it with an if statement at the end. For example, we can ask the user if he wants to continue, or N.

```
;if the answer is N, wait a while, and stop the semicolon.
```

Notice that it is not Logo, but pseudocode, so we put it in front of it.
Here's another way to do it: don't use forever at the top; just start the steps in the loop. Then at the end of the loop, ask the user if he wants to continue, or N. If the answer is Y, we call Main. If it is N, we don't. So we are calling Main from within Main. Sound strange? It works, as long as you have a get out of the loop.

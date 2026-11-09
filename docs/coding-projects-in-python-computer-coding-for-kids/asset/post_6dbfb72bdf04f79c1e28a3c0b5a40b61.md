
## Listening for presses

Finally, use `onkey()` to link the direction functions to the keyboard keys. Add these lines after the `onkey()` call you made in Step 9. When you start the code in place, the game's complete. Have fun playing and finding out your highest score!

```
t.onkey(start_game, 'space')
t.onkey(move_up, 'Up')
t.onkey(move_right, 'Right')
t.onkey(move_down, 'Down')
t.onkey(move_left, 'Left')
t.listen()
```

> Call the `move_up` function when the “up” key is pressed.

## Hacks and tweaks

Now that your caterpillar game is working, it won’t be too difficult to modify it or even introduce a helper or rival caterpillar!

## Make it a two-player game

By creating a second caterpillar turtle with separate keyboard controls, you and a friend can work together to make the caterpillar eat even more leaves!

![](img/6b18a113f7aa9338e32f3ac1fa217987_166_0.png)

- **1. Create a new caterpillar**

First you’ll need to add a new caterpillar. Type these lines near the top of your program, below the code that creates the first caterpillar.

```
caterpillar2 = t.Turtle()
caterpillar2.color('blue')
caterpillar2.shape('square')
caterpillar2.penup()
caterpillar2.speed(0)
caterpillar2.hideturtle()
```

- **2. Add a parameter**

To reuse the `outside_window()` function for both caterpillars, add a parameter to it. Now you can tell it which caterpillar you want it to check on.

```
def outside_window(caterpillar):
```

- **3. Hide caterpillar2**

When the `game_over()` function is called, it hides the first caterpillar. Let’s add a line to hide the second caterpillar as well.

```
def game_over():
    caterpillar.color('yellow')
    caterpillar2.color('yellow')
    leaf.color('yellow')
```

## Change the main function

You’ll need to add code for caterpillar2 to the main `start_game()` function. First set its starting shape and heading in the code snippet direction from the first caterpillar. Then add it to the `while` loop to make it move, and add the `if` statement to check if it has eaten the leaves. You’ll also need to add a line to make it grow. Finally, edit the call to the `outside_window()` function in your second `if` statement to see if the game is over.

![](img/6b18a113f7aa9338e32f3ac1fa217987_167_0.png)

```python
score = 0
text_turtle.clear()

caterpillar_speed = 2
caterpillar_length = 3
caterpillar.shapesize(1, caterpillar_length, 1)
caterpillar.showturtle()
caterpillar2.shapesize(1, caterpillar_length, 1)
caterpillar2.setheading(180)
caterpillar2.showturtle()
display_score(score)

while True:
    caterpillar.forward(caterpillar_speed)
    caterpillar2.forward(caterpillar_speed)
    if caterpillar.distance(leaf) < 20 or leaf.distance(caterpillar2) < 20:
        caterpillar_length = caterpillar_length + 1
        caterpillar.shapesize(1, caterpillar_length, 1)
        caterpillar2.shapesize(1, caterpillar_length, 1)
        caterpillar_speed = caterpillar_speed + 1
        score = score + 10
        display_score(score)
    if outside_window(caterpillar) or outside_window(caterpillar2):
        game_over()
```

This sets caterpillar2’s starting shape.

Caterpillar2 starts heading left.

Each time the program loops, caterpillar2 moves forward.

This checks if caterpillar2 has eaten the leaf.

Caterpillar2 gets longer.

Has caterpillar2 left the screen?

## Extra controls

Now assign the keys that the second player will use to control the new caterpillar. The code here uses 'w' for up, 'a' for left, 's' for down, and 'd' for right, but feel free to try out different choices. You'll need four new functions and four uses of onkey to tie the new keys to the new functions.

```python
def caterpillar2_move_up():
    if caterpillar2.heading() == 0 or caterpillar2.heading() == 180:
        caterpillar2.setheading(90)

def caterpillar2_move_down():
    if caterpillar2.heading() == 0 or caterpillar2.heading() == 180:
        caterpillar2.setheading(270)

def caterpillar2_move_left():
    if caterpillar2.heading() == 90 or caterpillar2.heading() == 270:
        caterpillar2.setheading(180)

def caterpillar2_move_right():
    if caterpillar2.heading() == 90 or caterpillar2.heading() == 270:
        caterpillar2.setheading(0)

t.onkey(caterpillar2_move_up, 'w')
t.onkey(caterpillar2_move_right, 'd')
t.onkey(caterpillar2_move_down, 's')
t.onkey(caterpillar2_move_left, 'a')
```

![](img/6b18a113f7aa9338e32f3ac1fa217987_168_0.png)

## Make it competitive

See if you can figure out how to adapt the two-player game to record each player's score and then declare the winner at the end. Here's a tip: you'll need a new variable to keep track of the second player's score. When a caterpillar eats a leaf, you'll need to add a point only to that caterpillar's score. Finally, when the game is over, you can compare the scores to see who's won.

## Make it harder or easier

If you alter the values inside the loop that increase the length (+1) and speed (+2) of the caterpillar, you can change the difficulty of the game. Higher numbers will make the game harder, while lower numbers will make it easier.

![](img/6b18a113f7aa9338e32f3ac1fa217987_168_1.png)

## Snap

Challenge your friends to a game of digital snap. This fast-paced, two-player game requires a sharp eye and lightning-fast reactions. It works just like the card game but uses colored shapes that appear on the screen rather than cards that are dealt.

### What happens

Different shapes appear on the screen at random in either black, red, green, or blue. If a color appears twice in succession, hit the snap key. Player 1 presses the “q” key to snap and player 2 the “p” key. Each correct snap scores a point. Snap at the wrong time and you lose a point. The player with the highest score is the winner.

### Starting the game

This game works on a Tkinter window. When you start the program, the Tkinter window might be hidden behind IDLE windows on your desktop. Move them out of the way so you can see the game. Be quick though: the snap shapes start appearing 3 seconds after you run the program.

![](img/6b18a113f7aa9338e32f3ac1fa217987_169_0.png)

This is a snap because the colors are the same, even though the shapes are different.

![](img/6b18a113f7aa9338e32f3ac1fa217987_169_1.png)

Although these shapes match, their colors are different, so it’s not a snap.

## How it works

This project uses Tkinter to create the shapes. Tkinter's mainloop() function schedules a function that you'll create to show the next shape. The random module's shuffle() function makes sure the shapes appear in a different order. The “q” and “p” keys are bound (linked) to a snap() function, so that each time one of these keys is pressed, it updates the relevant player's score.

### ▷ Snap flowchart

The program runs for as long as there are still shapes left to be revealed. It reacts to the key presses of the players when they think they see a snap. When there are no more shapes left, the winner is declared and the game ends.

## EXPERT TIPS

### Sleep

Computers work a lot faster than you can. Sometimes this causes problems. If you tell a computer to show a shape to the user and then hide it again, without a break, the computer does it so quickly that the person won't see the shape. To fix this, Snap uses the time module's sleep() function, which pauses a program for a set number of seconds: time.sleep(1), for example, puts the program to sleep for 1 second before it runs the next line of code.

![](img/6b18a113f7aa9338e32f3ac1fa217987_170_0.png)

## Getting started

First you need to import the relevant modules and create a graphical user interface (GUI). Then you need to create a canvas to draw the shapes on.

![](img/6b18a113f7aa9338e32f3ac1fa217987_171_0.png)

- **1. Create a new file**

Open IDLE. Create a new file and save it as “snap.py”.

- **2. Add modules**

First import the random and time modules, and parts of Tkinter. Time lets you create a delay so that the player is able to read a “SNAP!” or “WRONG!” message before the next shape is shown. HIDDEN lets you hide each shape until you want to show it with NORMAL—otherwise all the shapes will appear on the screen at the start of the game.

```python
import random

import time

from tkinter import Tk, Canvas, HIDDEN, NORMAL
```

You’ll shuffle the shapes using the random module.

Use Tkinter to create the GUI.

- **3. Set up the GUI**

Now type the code shown here to create a Tkinter window (also called a root widget) with the title “Snap”. Run the code to check it. The window may be hidden behind the other windows on the desktop.

```python
root = Tk()

root.title('Snap')
```

- **4. Create the canvas**

Type this line to create the canvas—the blank space on which the shapes will appear.

```python
c = Canvas(root, width=400, height=400)
```

## Making the shapes

The next stage is to create the colored shapes using functions from Tkinter’s Canvas widget. You’ll draw circles, squares, and rectangles, each in four different colors.

![](img/6b18a113f7aa9338e32f3ac1fa217987_171_1.png)

- **5. Make a store for the shapes**

You need to make a list so that you can store all the shapes somewhere. Add this line at the bottom of your file.

```python
shapes = []
```


## Filling in the blanks

It’s time to replace `pass` in the placeholder functions with actual code. After adding the code for each function, run the game to see what difference it makes.

### Stay inside

Fill the `outside_window()` function with this code. First it calculates the position of each of the walls. Then it asks the caterpillar for its current position. By comparing the caterpillar’s coordinates with the coordinates of the walls, it can tell whether the caterpillar has left the window. Run the program to check the function works – the caterpillar should stop when it reaches the edge.

```python
def outside_window():
    left_wall = -t.window_width() / 2
    right_wall = t.window_width() / 2
    top_wall = t.window_height() / 2
    bottom_wall = -t.window_height() / 2
    (x, y) = caterpillar.pos()
    outside = \
        x < left_wall or \
        x > right_wall or \
        y < bottom_wall or \
        y > top_wall
    return outside
```

> This function returns two values (a “tuple”).

> If any of the four conditions above is True, then outside is True.

![](img/1bd24ab186f69fb18194b4174ca15178_162_0.png)

### How it works

The centre of the window has the coordinates (0, 0). Since the window is 400 wide, the right wall is half the width from the centre, which is 200. The code gets the left wall’s position by subtracting half the width from 0. In other words, 0 - 200, which is -200. It finds the position of the top and bottom walls by a similar method.

### GAME OVER!

Now you know when the caterpillar has left the screen, display a message to tell the player the game has ended. Fill in the `game_over()` function with this code. When called, the function will hide the caterpillar and leaf, and write “GAME OVER!” on the screen.

![](img/1bd24ab186f69fb18194b4174ca15178_162_1.png)

```python
def game_over():
    caterpillar.color('yellow')
    leaf.color('yellow')
    t.penup()
    t.hideturtle()
    t.write('GAME OVER!', align='center', font=('Arial', 30, 'normal'))
```

> The text should be centred (Python uses the US spelling “center”).

### 13 Show the score

The function `display_score()` instructs the score turtle to rewrite the score, putting the latest total on the screen. This function is called whenever the caterpillar reaches a leaf.

```python
def display_score(current_score):
    score_turtle.clear()
    score_turtle.penup()
    x = (t.window_width() / 2) - 50
    y = (t.window_height() / 2) - 50
    score_turtle.setpos(x, y)
    score_turtle.write(str(current_score), align='right', \
                       font=('Arial', 40, 'bold'))
```

50 pixels from the right

50 pixels from the top

### 14 A new leaf

When a leaf is reached, the function `place_leaf()` is called to move the leaf to a new, random location. It chooses two random numbers between −200 and 200. These numbers become the x and y coordinates for the next leaf.

```python
def place_leaf():
    leaf.ht()
    leaf.setx(random.randint(-200, 200))
    leaf.sety(random.randint(-200, 200))
    leaf.st()
```

`ht` is short for hideturtle.

Chooses random coordinates to move the leaf.

`st` is short for showturtle.

### 15 Turning the caterpillar

Next, to connect the keyboard keys to the caterpillar, add four new direction functions after the `start_game()` function. To make this game a little trickier, the caterpillar can only make 90-degree turns. As a result, each function first checks to see which way the caterpillar is moving before altering its course. If the caterpillar is going the wrong way, the function uses `setheading()` to make it face the right direction.

```python
game_over()
    break

def move_up():
    if caterpillar.heading() == 0 or caterpillar.heading() == 180:
        caterpillar.setheading(90)

def move_down():
    if caterpillar.heading() == 0 or caterpillar.heading() == 180:
        caterpillar.setheading(270)

def move_left():
    if caterpillar.heading() == 90 or caterpillar.heading() == 270:
        caterpillar.setheading(180)

def move_right():
    if caterpillar.heading() == 90 or caterpillar.heading() == 270:
        caterpillar.setheading(0)
```

Check if the caterpillar is heading left or right.

A heading of 270 sends the caterpillar down the screen.

### 16 Listening for presses

Finally, use `onkey()` to link the direction functions to the keyboard keys. Add these lines after the `onkey()` call you made in Step 9. With the steering code in place, the game’s complete. Have fun playing and finding out your highest score!

```python
t.onkey(start_game, 'space')
t.onkey(move_up, 'Up')
t.onkey(move_right, 'Right')
t.onkey(move_down, 'Down')
t.onkey(move_left, 'Left')
t.listen()
```

> Call the `move_up` function when the “up” key is pressed.

## Hacks and tweaks

**Now that your caterpillar game is working, it won’t be too difficult to modify it or even introduce a helper or rival caterpillar!**

### Make it a two-player game

By creating a second caterpillar turtle with separate keyboard controls, you and a friend can work together to make the caterpillar eat even more leaves!

![](img/1bd24ab186f69fb18194b4174ca15178_164_0.png)

- **1 Create a new caterpillar**

First you’ll need to add a new caterpillar. Type these lines near the top of your program, below the code that creates the first caterpillar.

```python
caterpillar2 = t.Turtle()
caterpillar2.color('blue')
caterpillar2.shape('square')
caterpillar2.penup()
caterpillar2.speed(0)
caterpillar2.hideturtle()
```

- **2 Add a parameter**

To reuse the `outside_window()` function for both caterpillars, add a parameter to it. Now you can tell it which caterpillar you want it to check on.

```python
def outside_window(caterpillar):
```

- **3 Hide caterpillar2**

When the `game_over()` function is called, it hides the first caterpillar. Let’s add a line to hide the second caterpillar as well.

```python
def game_over():
    caterpillar.color('yellow')
    caterpillar2.color('yellow')
    leaf.color('yellow')
```

### Change the main function

You'll need to add code for caterpillar2 to the main `start_game()` function. First set its starting shape and make it face the opposite direction to the first caterpillar. Then add it to the `while` loop to make it move, and add a check to the `if` statement so it can eat the leaves. You'll also need to add a line to make it grow. Finally, edit the call to the `outside_window()` function in your second `if` statement to see if the game is over.

![](img/1bd24ab186f69fb18194b4174ca15178_165_0.png)

```python
score = 0
text_turtle.clear()

caterpillar_speed = 2
caterpillar_length = 3
caterpillar.shapesize(1, caterpillar_length, 1)
caterpillar.showturtle()

caterpillar2.shapesize(1, caterpillar_length, 1)  # This sets caterpillar2's starting shape.
caterpillar2.setheading(180)  # Caterpillar2 starts heading left.
caterpillar2.showturtle()
display_score(score)
place_leaf()

while True:
    caterpillar.forward(caterpillar_speed)
    caterpillar2.forward(caterpillar_speed)  # Each time the program loops, caterpillar2 moves forwards.
    if caterpillar.distance(leaf) < 20 or leaf.distance(caterpillar2) < 20:  # This checks if caterpillar2 has eaten the leaf.
        place_leaf()
        caterpillar_length = caterpillar_length + 1
        caterpillar.shapesize(1, caterpillar_length, 1)
        caterpillar2.shapesize(1, caterpillar_length, 1)  # Caterpillar2 gets longer.
        caterpillar_speed = caterpillar_speed + 1
        score = score + 10
        display_score(score)

    if outside_window(caterpillar) or outside_window(caterpillar2):  # Has caterpillar2 left the screen?
        game_over()
```

### Extra controls

Now assign the keys that the second player will use to control the new caterpillar. The code here uses “w” for up, “a” for left, “s” for down, and “d” for right, but feel free to try out different choices. You’ll need four new functions and four uses of onkey to tie the new keys to the new functions.

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

![](img/1bd24ab186f69fb18194b4174ca15178_166_0.png)

> “That’s an old photo of me winning the competition!”

### ▽ Make it harder or easier

If you alter the values inside the loop that increase the length (+1) and speed (+2) of the caterpillar, you can change the difficulty of the game. Higher numbers will make the game harder, while lower numbers will make it easier.

> “What I’m doing is way trickier!”

### △ Make it competitive

See if you can figure out how to adapt the two-player game to record each player’s score and then declare the winner at the end. Here’s a tip: you’ll need a new variable to keep track of the second player’s score. When a caterpillar eats a leaf, you’ll need to add a point only to that caterpillar’s score. Finally, when the game is over, you can compare the scores to see who’s won.

![](img/1bd24ab186f69fb18194b4174ca15178_166_1.png)

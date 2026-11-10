
Finally, add this just above the last line in the main part of the program to get `mainloop()` to call `change_color()` 5 seconds (5,000 milliseconds) after the program starts.

```
root.after(5000, change_color)
```

Your pet will begin changing colour 5 seconds after the program starts.

- 4. You might want to alter the values in the code so that Screen Pet changes colour less rapidly. You could also change the colours in the list to ones you like better, or add extra colours.

![](img/1bd24ab186f69fb18194b4174ca15178_154_0.png)

## Feed me!

Pets need food, as well as stroking and tickling. Can you figure out ways to feed your pet and keep it healthy?

- 1. Perhaps try adding a “Feed me!” button to Screen Pet’s window and a `feed()` function that’s called when you click the button.

- 2. You could even make Screen Pet grow if you click “Feed me!” a certain number of times. This line of code makes its body bigger.

![](img/1bd24ab186f69fb18194b4174ca15178_154_1.png)

```
body = c.create_oval(15, 20, 395, 350, outline=c.body_color, fill=c.body_color)
```

This code reshapes the oval that makes up Screen Pet’s body.

- 3. Then try writing some code so that your pet’s body shrinks back to its original size again if it doesn’t get enough food.

### Clean that up!

The problem with feeding Screen Pet is that it will need to poo as well! Write some code that makes it poo a while after you feed it. Then add a “Clean up” button. Clicking “Clean up” should call a handler function that removes the poo.

![](img/1bd24ab186f69fb18194b4174ca15178_154_2.png)

![](img/1bd24ab186f69fb18194b4174ca15178_154_3.png)

## Games in Python

![](img/1bd24ab186f69fb18194b4174ca15178_156_0.png)

## Caterpillar

If all this coding has worked up your appetite, you're not alone – the star of this project is a hungry caterpillar. Using Python's turtle module, you'll find out how to animate game characters and control them on screen with the keyboard.

![](img/1bd24ab186f69fb18194b4174ca15178_157_0.png)

> Maybe it's time you turned over a new leaf!

### What happens

You use the four arrow keys to steer a caterpillar around the screen and make it "eat" leaves. Each leaf gives you a point, but it also makes the caterpillar bigger and faster, making the game harder. Keep the caterpillar inside the game window, or it's game over!

![](img/1bd24ab186f69fb18194b4174ca15178_157_1.png)

Python Turtle Graphics 20

Your score is displayed in the top-right corner of the game window.

The leaf disappears when eaten, and a new leaf then appears elsewhere.

To start the game, the player has to click on the screen first and then press the space-bar.

### Increasing difficulty

The more leaves the caterpillar eats, the harder the game becomes. As the caterpillar gets longer and faster, your reactions have to speed up too, otherwise your caterpillar will zoom off the screen.

## Writing SQL Queries

A query is a question you ask the database. SQL (Structured Query Language) is used to retrieve data from databases. The most common command is SELECT.

- SELECT: retrieves data from one or more tables
- FROM: specifies the table(s) to query
- WHERE: filters records based on conditions
- ORDER BY: sorts the result set

```sql
SELECT first_name, last_name
FROM employees
WHERE department = 'Engineering'
ORDER BY last_name;
```

Note: Always use semicolons at the end of SQL statements. Use single quotes for string literals. Be mindful of NULL values in WHERE clauses.

### 3 Create a caterpillar turtle

Now create the turtle that will become your caterpillar. Add the code shown here. It creates the turtle and sets its colour, shape, and speed. The function caterpillar.penup() disables the turtle's pen, allowing you to move the turtle around the screen without drawing a line along the way.

```python
caterpillar = t.Turtle()
caterpillar.shape('square')
caterpillar.color('red')
caterpillar.speed(0)
caterpillar.penup()
caterpillar.hideturtle()
```

Create a new turtle for the caterpillar.

We don't want the turtle to move before the game starts.

This command hides the turtle.

### 4 Create a leaf turtle

Below the code for Step 3, type these lines to set up the second turtle, which will draw the leaves. The code uses a list of six coordinate pairs to draw a leaf shape. Once you tell the turtle about this shape, it can reuse the details to draw more leaves. A call to hideturtle here makes this turtle invisible on the screen.

```python
leaf = t.Turtle()
leaf_shape = ((0, 0), (14, 2), (18, 6), (20, 20), \
              (6, 18), (2, 14))
t.register_shape('leaf', leaf_shape)
leaf.shape('leaf')
leaf.color('green')
leaf.penup()
leaf.hideturtle()
leaf.speed(0)
```

This turtle will draw the leaves.

The coordinates for leaf shape

Use a backslash character if you need to split a long line of code over two lines.

This line tells the turtle about the leaf shape.

### 5 Add some text

Now set up two more turtles to add text to the game. One will display a message before the action starts, telling players to press space-bar to begin. The other will write the score in the corner of the window. Add these lines after the leaf turtle code.

```python
game_started = False
text_turtle = t.Turtle()
text_turtle.write('Press SPACE to start', align='center', \
                  font=('Arial', 16, 'bold'))
text_turtle.hideturtle()
score_turtle = t.Turtle()
score_turtle.hideturtle()
score_turtle.speed(0)
```

You'll need to know later if the game has started.

This line draws some text on the screen.

This hides the turtle but not the text.

Add a turtle to write the score.

The turtle needs to stay where it is, so that it can update the score.

### Main loop

Your turtles are now set up and ready to go. Let's write the code that makes the game come to life.

### 6 Placeholder functions

You can put off defining a function until later by using the pass keyword. Under the code for the turtles, add the following placeholder functions for functions that you'll fill with code in later steps.

```
def outside_window():
    pass

def game_over():
    pass

def display_score(current_score):
    pass

def place_leaf():
    pass
```

To get a basic version of the program running sooner, you can use placeholders for functions that you'll finish coding later.

### EXPERT TIPS

### Pass

In Python, if you're not yet sure what code you want inside a function, you can just type in the pass keyword and then come back to it later. It's a bit like passing on a question in a quiz.

### 7 Game starter

After the four placeholder functions comes the start_game() function, which sets up some variables and prepares the screen before the main animation loop begins. You'll add the code for the main loop, which forms the rest of this function, in the next step.

The turtle stretches into a caterpillar shape.

![](img/1bd24ab186f69fb18194b4174ca15178_160_0.png)

```
def start_game():
    global game_started
    if game_started:
        return
    game_started = True

    score = 0
    text_turtle.clear()

    caterpillar_speed = 2
    caterpillar_length = 3
    caterpillar.shapesize(1, caterpillar_length, 1)
    caterpillar.showturtle()
    display_score(score)
    place_leaf()
```

If the game has already started, the return command makes the function quit so it doesn't run a second time.

Clear the text from the screen.

This line places the first leaf on the screen.

### 8 Get moving

The main loop moves the caterpillar forwards slightly, before performing two checks. It first checks if the caterpillar has reached the leaf. If the leaf has been eaten, the score increases, a new leaf gets drawn, and the caterpillar gets longer and faster. The loop then checks if the caterpillar has left the window - if so, the game's over. Add the main loop below the code you typed in Step 7.

> The very hungry what? No, I've never heard of him!

![](img/1bd24ab186f69fb18194b4174ca15178_161_0.png)

```python
place_leaf()

while True:
    caterpillar.forward(caterpillar_speed)
    if caterpillar.distance(leaf) < 20:
        place_leaf()
        caterpillar_length = caterpillar_length + 1
        caterpillar.shapesize(1, caterpillar_length, 1)
        caterpillar_speed = caterpillar_speed + 1
        score = score + 10
        display_score(score)
    if outside_window():
        game_over()
        break
```

The caterpillar eats the leaf when it's less than 20 pixels away.

The current leaf has been eaten, so add a new leaf.

This will make the caterpillar grow longer.

### 9 Bind and listen

Now put these lines below the function you've just created. The onkey() function binds the space-bar to start_game(), so you can delay the start until the player presses space. The listen() function allows the program to receive signals from the keyboard.

```python
t.onkey(start_game, 'space')
t.listen()
t.mainloop()
```

When you press the space-bar, the game begins.

### 10 Test your code

> My caterpillar crawled off the screen and into the garden!

Run the program. If your code is correct, you should see the caterpillar moving after you press the space-bar. Eventually, it should crawl off the screen. If the program doesn't work, check your code carefully for bugs.

![](img/1bd24ab186f69fb18194b4174ca15178_161_1.png)


## 11 Using placeholders

You need to write some more functions in order to finish the game. You can add function placeholders without having to define them right away by using the keyword `pass`. Type in this code to give yourself a template of the functions you'll need.

```python
coin.draw()
screen.draw.text("Score: " + str(score), color="black", topleft=(10, 10))
```

```python
def place_coin():
    pass

def time_up():
    pass

def update():
    pass
```

To get an idea of the code's structure you can use placeholders for functions that you'll finish coding later.

![](img/3188b147f991a51de14dcd2bb4b4c42e_65_0.png)

## 12 Importing randint()

Now it's time to define these functions. The first one will use Python's built-in `randint()` function, so you need to import it into your program. Type this line at the very top of your code to import it.

```python
from random import randint
```

Make sure you type this before all the code you've written so far.

## 13 Placing the coin

Next change the code in your `place_coin()` function. This function will place the coin in a random position on the screen. Delete `pass` and type in these commands.

```python
def place_coin():
    coin.x = randint(20, (WIDTH - 20))
    coin.y = randint(20, (HEIGHT - 20))
```

The coin will be placed at least 20 pixels in from the sides of the screen.

## 14 Run the function

Remember, it's not enough just to define the function; you have to run it, too. Add this line of code to the very bottom of your game.

```python
def update():
    pass

place_coin()
```

This will run the code you've saved in the `place_coin()` function.

### EXPERT TIPS

**Pass**

In Python, if you're not sure what code you want inside a function yet, you can use the `pass` keyword in its place, and then come back to it later. It's a bit like skipping a question in a quiz but answering it later.

## 15. Time's up!

Now let's fill in the code for the `time_up()` function. In this function, set the `game_over` Boolean variable to `True`, which will tell the program to quit the game when the function is called. Type in the following code.

```python
def time_up():
    global game_over
    game_over = True
```

Remember to delete the `pass` keyword and then add these lines.

## 16. Set the timer

Now that `time_up()` is defined, the program needs to run it. But it needs to run seven seconds after the game starts. You can use Pygame Zero's built-in tool `clock` to do this. This tool lets you program the call a function after a specified amount of time. Add this line in the code as shown here.

```python
clock.schedule(time_up, 7.0)
place_coin()
```

This line will run the function `time_up()` seven seconds after the game starts.

## 17. Ending the game

The game starts and then seven seconds later, `clock.schedule` will run the `time_up()` function, which ends the game. But the game still needs to show the player's final score. For this, you need to add in one more bit of code to the `draw()` function.

![](img/3188b147f991a51de14dcd2bb4b4c42e_66_0.png)

```python
def draw():
    screen.fill("green")
    fox.draw()
    coin.draw()
    screen.draw.text("Score: " + str(score), color="black", topleft=(10, 10))

    if game_over:
        screen.fill("pink")
        screen.draw.text("Final Score: " + str(score), topleft=(10, 10), fontsize=60)
```

If the variable `game_over` is `True`, this will turn the screen pink.

The final score is shown on the screen.

This command sets the size of the text shown on the screen.

## 18. Using update()

The final function you need to define is `update()`. This is a built-in Pygame Zero function, which means that unlike the other functions, you don't need to worry about when to run it. Once you've defined it, Pygame Zero will run it automatically—60 times a second! Delete `pass` under `def update()` and add this code. It will move the fox to the left if the left keyboard arrow is pressed.

```python
def update():
    if keyboard.left:
        fox.x = fox.x - 2
```

This moves the fox two pixels to the left if the left arrow is pressed.

## 19 One way only

Now test your code. You should be able to move the fox to the left. But the fox needs to be able to move in other directions, too, so add this code to do that.

![](img/3188b147f991a51de14dcd2bb4b4c42e_67_0.png)

```python
def update():
    if keyboard.left:
        fox.x = fox.x - 2
    elif keyboard.right:
        fox.x = fox.x + 2
    elif keyboard.up:
        fox.y = fox.y - 2
    elif keyboard.down:
        fox.y = fox.y + 2
```

The else-if branches are used to move the fox depending on which arrow key is pressed.

## 20 Collect the coins

Finally, you need to add some code that will update the score if the fox touches a coin. Add this code to the `update()` function.

Make sure you add this line at the very top.

If the fox touches the coin, this variable will be `True`.

```python
def update():
    global score

    if keyboard.left:
        fox.x = fox.x - 2
    elif keyboard.right:
        fox.x = fox.x + 2
    elif keyboard.up:
        fox.y = fox.y - 2
    elif keyboard.down:
        fox.y = fox.y + 2

    coin_collected = fox.colliderect(coin)

    if coin_collected:
        score = score + 10
        place_coin()

clock.schedule(time_up, 7.0)
place_coin()
```

This will increase the score by ten.

## 21 Game complete!

You've written all the code, and your game is now ready to go! Test your game and see how many coins you can collect before the game is over.

![](img/3188b147f991a51de14dcd2bb4b4c42e_67_1.png)

## Hacks and tweaks

There are lots of ways to modify your game. You could try changing the fox to a different character of your choice, or you could make the game last longer.

![](img/3188b147f991a51de14dcd2bb4b4c42e_68_0.png)

### △ A different Actor

You can replace the fox with some other character by using another image from the Python Games Resource Pack, or you can use the 8-bit editors available online to make your own Actor. Remember to update the code so it uses the name of the new character throughout the program.

![](img/3188b147f991a51de14dcd2bb4b4c42e_68_1.png)

```python
hedgehog = Actor("hedgehog")
```

### △ Extra time

The game currently ends after seven seconds. To make the game easier, you could give the player more time to play. You can do this by changing just one line of code.

![](img/3188b147f991a51de14dcd2bb4b4c42e_68_2.png)

![](img/3188b147f991a51de14dcd2bb4b4c42e_68_3.png)

```python
clock.schedule(time_up, 15.0)
```

### △ Change the playing area

You can change the size of the playing area by changing the values of `WIDTH` and `HEIGHT`. Try using different numbers for these values and see what happens. Can you spot which part of the code you need to update?

### △ Go faster!

You can tweak the code to make the fox move faster. For this, you'll need to change some of the code in the `update()` function. At the moment, the fox moves two pixels every time the arrows are pressed. Here's a way to make it move at double that speed.

```python
if keyboard.left:
    fox.x = fox.x - 4
elif keyboard.right:
    fox.x = fox.x + 4
elif keyboard.up:
    fox.y = fox.y - 4
elif keyboard.down:
    fox.y = fox.y + 4
```

![](img/3188b147f991a51de14dcd2bb4b4c42e_69_0.png)

## Follow the Numbers

![](img/3188b147f991a51de14dcd2bb4b4c42e_70_0.png)

## How to build

### Follow the Numbers

Can you connect all the dots in the correct order? Challenge yourself to finish the game as quickly as you can. Be careful, however—one wrong click and you'll have to start all over again.

### What happens

At the beginning of the game, ten dots appear at random positions on the screen, each with a number next to it. You need to click on the dots in the correct order to connect them. The game will finish once you've connected all the dots together. But if you make a mistake, all the lines will disappear and you'll have to start from the very first dot again.

![](img/3188b147f991a51de14dcd2bb4b4c42e_71_0.png)

![](img/3188b147f991a51de14dcd2bb4b4c42e_71_1.png)

### ◁ Dots and lines

The dots appear at random positions on the screen. When you click on the correct dot, a line will be drawn between it and the previous dot you clicked on.

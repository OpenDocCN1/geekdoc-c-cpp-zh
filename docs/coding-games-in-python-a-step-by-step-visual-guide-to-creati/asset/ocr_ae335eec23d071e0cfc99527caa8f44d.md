# Random numbers

Your program needs to generate dance sequences for you to memorize and repeat. The four possible moves are **Up**, **Down**, **Left**, and **Right**. You don’t have a function that will generate random directions, but the `random()` function will let you generate random numbers. If you assign each move a number, starting from 0 you will then be able to create random dance sequences. Step 15 will show you how to do this.

![](bbox=[0.577, 0.052, 0.893, 0.242])

# Let’s move!

The first function you need to define properly is `update_dancer()`. This changes the image of the dancer to match the dance move he should perform. The colored square that corresponds to that move changes to become outlined in yellow. Replace `pass` under the `update_dancer()` function from Step 13 with the code shown below. There’s quite a lot to add, so be extra careful!

![](bbox=[0.833, 0.294, 0.951, 0.414])

Don’t forget to save your work.

```
```python
def update_dancer(move):
    global game_over
    if not game_over:
        if move == 0:
            up.image = "up-lit"
            dancer.image = "dancer-up"
            clock.schedule(reset_dancer, 0.5)
        elif move == 1:
            right.image = "right-lit"
            dancer.image = "dancer-right"
            clock.schedule(reset_dancer, 0.5)
        elif move == 2:
            down.image = "down-lit"
            dancer.image = "dancer-down"
            clock.schedule(reset_dancer, 0.5)
        else:
            left.image = "left-lit"
            dancer.image = "dancer-left"
            clock.schedule(reset_dancer, 0.5)
    return
```
```

This line tells Python which global variable to use.

This line highlights the colored square for Up with a yellow outline.

This function will tell the dancer which move to perform.

The value in `move` tells the dancer which dance move to do. Here, it’s set to 0, which will mean Up.

This line changes the image of the dancer.

The dancer will hold the move for half a second before `reset_dancer()` is called, returning him to the starting pose.

![](bbox=[0.768, 0.847, 0.968, 0.995])
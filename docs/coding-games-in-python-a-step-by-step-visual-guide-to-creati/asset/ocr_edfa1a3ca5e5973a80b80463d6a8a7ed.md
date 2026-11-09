![](bbox=[0.021, 0.095, 0.946, 0.294])

# ▷ **In record time**

You can use the system clock to time how long it takes a player to connect all the dots. You could then try to beat your friends’ times! To time the game, you’ll need to use the `time()` function. Once the game is complete, you can display the final time taken on the screen. Why not try placing the clock in the corner? Remember to use `str()` to cast the message into a string. You can check Step 9 of the page if you need to remind yourself how to do this. At the moment, though, the `draw()` function is only called when the player clicks the mouse, so the clock would only update after each mouse click. To fix this, add this code. This function is called 60 times a second. Each call also calls the `draw()` function, so the clock stays up to date.

```
```python
from time import time
```
```

Put this code at the top of your program to use the Time module.

```
```python
def update():
    pass
```
```

You don’t need to replace `pass` with any actual code.

# **EXPERT TIPS**

# ## `time()`

The `time()` function might give you an unexpected result. It calculates the time that’s passed since an “epoch,” which is the date an operating system considers to be the “start of time.” Windows machines will tell you how many seconds have passed since January 1, 1601! You can use this simple calculation below to work out how long it actually took the player to complete the game.

```
```python
total_time = end_time - start_time
```
```

This calculates the total time elapsed.

# **EXPERT TIPS**

# ## `round()`

The `time()` function calculates time to lots of decimal places. You can use the `round()` function to round it to a certain number of decimal places, which will make it easier to read. `round()` takes two parameters—the number to round up or down and the number of decimal places to shorten it to.

```
```python
>>> round(5.75, 1)
5.8
```
```

This is the number of decimal places you want to round it to.

This is the number you want to round up.
```
```python
def draw_circle(size, angle, shift):
    turtle.bgcolor(next(colors))
    turtle.pencolor(next(colors))
    turtle.circle(size)
    turtle.right(angle)
    turtle.forward(shift)
    draw_circle(size + 5, angle + 1, shift + 1)


turtle.speed('fast')
turtle.pensize(4)
draw_circle(30, 1, 1)
```
```

> The background color is now set inside the loop.

# ▽ Find new patterns

The appearance of the pattern is determined by how much you add to the function's parameters each time it's called. Try adding more or less to the size, shift, and angle than you do at the moment, to find out how these changes affect the pattern.

# < Crazy colors

What if you change the background color on each loop, as well as the pen color? It might give you some wild results! To get the background color to change each time, move the line that sets it into the draw_circle() function. You'll also need to use the color cycle to select a new color on each loop.

![](bbox=[0.069, 0.701, 0.491, 0.955])

Size +10, angle +10, shift +1

![](bbox=[0.567, 0.701, 0.993, 0.955])

Size +5, angle +20, shift -10
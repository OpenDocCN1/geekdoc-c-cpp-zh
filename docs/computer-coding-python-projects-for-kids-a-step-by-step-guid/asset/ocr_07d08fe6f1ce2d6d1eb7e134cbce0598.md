# EXPERT TIPS

# Recursion

When a function calls itself, this is known as recursion. It's another way of making a loop in your program. In most uses of recursion, the parameters of the function change each time the function is called. In Kaleido-spiral, for example, the size, angle, and position of the circle change whenever the function calls itself.

![](bbox=[0.04, 0.24, 0.49, 0.45])

# 6. Test your code

Run the program. You would see the turtle drawing the same circle over and over again. Don't worry - you'll fix that in the next step.

![](bbox=[0.55, 0.16, 0.99, 0.57])

# 7. Change the colour, increase the size

To create more exciting patterns, make these changes to the code to increase the size of the circle and change its colour. This code uses the cycle() function, which takes a list of values as its parameter and returns a special type of list that you can cycle through endlessly using the next() function. Run the code again.

```
    import turtle
    from itertools import cycle

    colors = cycle(['red', 'orange', 'yellow', 'green', 'blue', 'purple'])

    def draw_circle(size):
        turtle.pencolor(next(colors))
        turtle.circle(size)
        draw_circle(size + 5)

    turtle.bgcolor('black')
    turtle.speed('fast')
    turtle.pensize(4)
    draw_circle(30)
```

Import the cycle() function.

This line creates a cycle of the colours in the list.

Use the next colour in the cycle.

Add 5 to the previous circle size.
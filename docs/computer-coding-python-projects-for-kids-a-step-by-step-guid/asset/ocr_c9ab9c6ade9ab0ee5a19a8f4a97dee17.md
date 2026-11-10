# Define thickness

In this step, you’ll create a function that will let the user choose whether the turtle paints superthick, thick, or thin lines. Like the `get_line_length()` function, you won’t use it until Step 5. Type the code shown here, under the code you added in Step 3.

```
return line_length

def get_line_width():
    choice = input('Enter line width (superthick, thick, thin): ')
    if choice == 'superthick':
        line_width = 40
    elif choice == 'thick':
        line_width = 25
    else:
        line_width = 10
    return line_width
```

This asks the user to choose how thick the line is.

If short lines are chosen, this sets `line_width` to 10.

This command passes `line_width` back to the code that used this function.

# Use the functions

Now you’ve built the two functions, you can use them to get the user’s choices for line length and width. Type these lines at the end of your code, then save your work.

```
return line_width

line_length = get_line_length()
line_width = get_line_width()
```

# Test the program

Run the code to see the new functions in action in the shell. They’ll ask you to select the length and width of the lines.

```
Enter line length (long, medium, short): long
Enter line width (superthick, thick, thin): thin
```

User input

# Summon the turtle!

It’s time to write the code that will create a graphics window and bring the turtle in to do the drawing.

![](bbox=[0.512, 0.674, 0.702, 0.785])

# Open a window

Type the lines shown here under the code you added in Step 5. This code defines the background colour of the window, the shape, colour, and speed of the turtle, as well as the width of the pen the turtle will use to draw lines.

```
line_width = get_line_width()

t.shape('turtle')
t.fillcolor('green')
t.bgcolor('black')
t.speed('fastest')
t.pensize(line_width)
```

The turtle’s standard shape is an arrowhead. This changes it to a turtle shape.

This makes the turtle green.

This sets the background to black.

This sets the turtle’s speed.

This sets the pen’s width to the user’s choice.
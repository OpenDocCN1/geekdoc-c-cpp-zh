![](bbox=[0.057, 0.057, 0.478, 0.238])

# ◁ Runaway turtle!

Given complete freedom to roam, the turtle tends to wander out of the window. As you put the program together, you’ll write some code to check on the turtle’s position and stop it from straying too far. Otherwise, this will turn into a vanishing turtle project!

# Getting started

Start by setting up and saving a new file, importing the modules that the program will need, and making a couple of useful functions to get user input.

![](bbox=[0.008, 0.442, 0.502, 0.553])

+   1. **Create new files**  
+      Open IDLE and create a new file. Save it as `rainbow.py`.
+   
+   2. **Add the modules**  
+      Type these two lines at the top of your file to import the Turtle module and the random module. Remember to `import turtle as t`, so that you don’t have to type the word “turtle” every time you want to use a function from the Turtle module. You can just call it `t`.

```
```python
import random
import turtle as t
```
```

![](bbox=[0.019, 0.602, 0.063, 0.644])

# Assign line length

Next make a function that will let the user decide whether the turtle paints long, medium, or short lines. You won’t use it until Step 4, but this will get the program ready for when you need it. Type this bit of code beneath the code in Step 1.

```
```python
def get_line_length():
    choice = input('Enter line length (long, medium, short): ')
    if choice == 'long':
        line_length = 250
    elif choice == 'medium':
        line_length = 200
    else:
        line_length = 100
    return line_length
```
```

This asks the user to choose how long the line is.

For a short line, set `line_length` to 100.

This command passes `line_length` back to the code that called this function.
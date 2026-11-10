
## Hacks and tweaks

**Are your rainbows mutant enough? No? Here are some ideas you could try to make them even more bizarre!**

![](img/1bd24ab186f69fb18194b4174ca15178_104_0.png)

### Colour surprise!

In Python, colours can also be described by using RGB values – this stands for red, green, blue. Choosing values at random for the amounts of red, green, and blue in a colour means the colour itself will be completely random. Try replacing the code in the `move_turtle()` function with some new code that uses RGB values instead of colour names. Now run the code to see what colours appear!

Replace these two lines with...

```python
    pen_colors = ['red', 'orange', 'yellow', 'green', 'blue', 'purple']
    t.pencolor(random.choice(pen_colors))
```

...these five lines.

```python
    t.colormode(255)
    red = random.randint(0, 255)
    green = random.randint(0, 255)
    blue = random.randint(0, 255)
    t.pencolor(red, green, blue)
```

### Mix up the lines

Don't just stick to one width for the line – draw even more scrambled rainbows with this hack! The lines will change at random from really thin to superthick and all widths in between. Add this code to the `move_turtle()` function after you set `t.pencolor`.

```python
    t.pensize(random.randint(1,40))
```

**EXPERT TIPS**

### RGB colours

In turtle, the colour “blue” is (0, 0, 255) in RGB values, as it’s made up of the maximum amount of blue, with no red or green. If you want to use RGB values for the turtle’s pen colour, you need to let Python know by using the command `t.colormode(255)`, or it will expect a string and give you an error.

This number shows the amount of red in the colour (between 0 and 255).

```python
    t.pencolor(0, 0, 255)
```

The amount of green

The amount of blue

```python
    t.pencolor('blue')
```

### Stamp the turtle!

Rivet the lines of your rainbows together by using the turtle module's `stamp()` function to add a turtle picture to the beginning of each line. (You could also write a function to draw a line entirely made up of stamped turtles and use it instead of `t.forward` and `t.backward`.) Add these new lines of code to the `move_turtle()` function, after the pen commands, to start riveting.

![](img/1bd24ab186f69fb18194b4174ca15178_105_0.png)

The turtle stamps look like rivets holding the lines together.

```python
def move_turtle(line_length):
    pen_colors = ['red', 'orange', 'yellow', 'green', 'blue', 'purple']
    t.pencolor(random.choice(pen_colors))
    t.fillcolor(random.choice(pen_colors))
    t.shapesize(3,3,1)
    t.stamp()
    if inside_window():
```

Type this to stamp a turtle picture on the screen.

This sets the colour of the turtle to a random colour.

This makes the turtle three times bigger than usual.

### Big or small turns?

You can add a prompt that allows the user to decide the angle of the turns the turtle makes. They can be wide, square, or narrow. Follow these steps to see how this changes the patterns.

**1. Make a function**

Create a function that lets the user choose the size of a turn. Add this above the `get_line_length()` function you added in Step 3 of the main project.

Type this to get the user's choice of turn angle.

```python
import turtle as t

def get_turn_size():
    turn_size = input('Enter turn size (wide, square, narrow): ')
    return turn_size


def get_line_length():
```

![](img/1bd24ab186f69fb18194b4174ca15178_105_1.png)

![](img/1bd24ab186f69fb18194b4174ca15178_105_2.png)

**2. Different moves**

Replace the `move_turtle()` function with the new version shown here. It adds `turn_size` to the values you pass to the function when you use it. It also replaces the line `angle = random.randint(0, 180)` with code that chooses different degrees to turn depending on the value of `turn_size`.

```python
def move_turtle(line_length, turn_size):
    pen_colors = ['red', 'orange', 'yellow', 'green', \
    'blue', 'purple']
    t.pencolor(random.choice(pen_colors))
    if inside_window():
        if turn_size == 'wide':
            angle = random.randint(120, 150)
        elif turn_size == 'square':
            angle = random.randint(80, 90)
        else:
            angle = random.randint(20, 40)
        t.right(angle)
        t.forward(line_length)
    else:
        t.backward(line_length)
```

- Square turns are between 80 and 90 degrees.
- Narrow turns are between 20 and 40 degrees.
- Wide turns are between 120 and 150 degrees.

**3. User input**

Next add a line to the main part of the program to use the `get_turn_size()` function to get the player's choice of turn size.

```python
line_length = get_line_length()
line_width = get_line_width()
turn_size = get_turn_size()
```

**4. Main program**

Finally, change the line where you use the `move_turtle()` function to include `turn_size`.

```python
while True:
    move_turtle(line_length, turn_size)
```

![](img/1bd24ab186f69fb18194b4174ca15178_106_0.png)

![](img/1bd24ab186f69fb18194b4174ca15178_106_1.png)

![](img/1bd24ab186f69fb18194b4174ca15178_106_2.png)

## Playful apps

![](img/1bd24ab186f69fb18194b4174ca15178_108_0.png)

## How it works

The program learns about the important events by reading information from a text file – this is called “file input”. The text file contains the name and date of each event. The code calculates the number of days from today until each event using Python’s `datetime` module. It displays the results in a window created by Python’s Tkinter module.

### Using Tkinter

The Tkinter module is a set of tools that Python programmers use for displaying graphics and getting input from users. Instead of showing output in the shell, Tkinter can display results in a separate window that you’re able to design and style yourself.

![](img/1bd24ab186f69fb18194b4174ca15178_110_0.png)

### LINGO

**Graphical user interface**

A GUI (graphical user interface) is the visible part of a program you interact with, such as the system of icons and menus on a smartphone. Python’s Tkinter module allows you to build a GUI by using what we call widgets – packages of ready-made code that create pop-up windows, buttons, sliders, menus and so on.

![](img/1bd24ab186f69fb18194b4174ca15178_110_1.png)

A smartphone GUI uses icons to show how strong the WiFi signal is and how much power the battery has.

## Countdown Calendar flowchart

In this project, the list of important events is created separately from the code as a text file. The program begins by reading in all the events from this file. Once all the days have been calculated and displayed, the program ends.

![](img/1bd24ab186f69fb18194b4174ca15178_110_2.png)

## Making and reading the text file

All the information for your Countdown Calendar must be stored in a text file. You can create it using IDLE.

![](img/1bd24ab186f69fb18194b4174ca15178_111_0.png)

### Create a new file

Open a new IDLE file, then type in a few upcoming events that are important to you. Put each event on a separate line and type a comma between the event and its date. Make sure there is no space between the comma and the event date.

Example contents of `events.txt`:

```text
Halloween,31/10/17
Spanish Test,01/12/17
School Trip,20/02/18
My Birthday,11/01/18
```

Type the date as day/month/year.

The name of the event comes first.

![](img/1bd24ab186f69fb18194b4174ca15178_111_1.png)

### Save it as a text file

Next save the file as a text file. Click the File menu, choose Save As, and call the file “events.txt”. Now you’re ready to start coding the Python program.

![](img/1bd24ab186f69fb18194b4174ca15178_111_2.png)

### Open a new Python file

You now need to create a new file for the code. Save it as “countdown_calendar.py” and make sure it’s in the same folder as your “events.txt” file.

![](img/1bd24ab186f69fb18194b4174ca15178_111_3.png)

### Set up the modules

This project needs two modules: `Tkinter` and `datetime`. Tkinter will be used to build a simple GUI, while datetime will make it easy to do calculations using dates. Import them by typing these two lines at the top of your new program.

```python
from tkinter import Tk, Canvas
from datetime import date, datetime
```

Import the Tkinter and datetime modules.

![](img/1bd24ab186f69fb18194b4174ca15178_111_4.png)


```python
game_font = font.nametofont('TkFixedFont')
game_font.config(size=18)

score = 0
score_text = c.create_text(10, 10, anchor='nw', font=game_font, fill='darkblue', \
                           text='Score: ' + str(score))

lives_remaining = 3
lives_text = c.create_text(canvas_width - 10, 10, anchor='ne', font=game_font, fill='darkblue', \
                           text='Lives: ' + str(lives_remaining))

eggs = []

def create_egg():
    x = randrange(10, 740)
    y = 40
    new_egg = c.create_oval(x, y, x + egg_width, y + egg_height, fill=next(color_cycle), width=0)
    eggs.append(new_egg)
    root.after(egg_interval, create_egg)

def move_eggs():
    for egg in eggs:
        (egg_x, egg_y, egg_x2, egg_y2) = c.coords(egg)
        c.move(egg, 0, 10)
        if egg_y2 > canvas_height:
            egg_dropped(egg)
    root.after(egg_speed, move_eggs)

def egg_dropped(egg):
    eggs.remove(egg)
    c.delete(egg)
    lose_a_life()
    if lives_remaining == 0:
        messagebox.showinfo('Game Over!', 'Final Score: ' + str(score))
        root.destroy()

def lose_a_life():
    global lives_remaining
    lives_remaining -= 1
    c.itemconfigure(lives_text, text='Lives: ' + str(lives_remaining))

def check_catch():
    (catcher_x, catcher_y, catcher_x2, catcher_y2) = c.coords(catcher)
    for egg in eggs:
        (egg_x, egg_y, egg_x2, egg_y2) = c.coords(egg)
        if catcher_x < egg_x and egg_x2 < catcher_x2 and catcher_y2 - egg_y2 < 40:
            eggs.remove(egg)
            c.delete(egg)
            increase_score(egg_score)

root.after(100, check_catch)

def increase_score(points):
    global score, egg_speed, egg_interval
    score += points
    egg_speed = int(egg_speed * difficulty_factor)
    egg_interval = int(egg_interval * difficulty_factor)
    c.itemconfigure(score_text, text='Score: ' + str(score))

def move_left(event):
    (x1, y1, x2, y2) = c.coords(catcher)
    if x1 > 0:
        c.move(catcher, -20, 0)

def move_right(event):
    (x1, y1, x2, y2) = c.coords(catcher)
    if x2 < canvas_width:
        c.move(catcher, 20, 0)

c.bind('<Left>', move_left)
c.bind('<Right>', move_right)
c.focus_set()

root.after(1000, create_egg)
root.after(1000, move_eggs)
root.after(1000, check_catch)
root.mainloop()
```

## Glossary

- **ASCII** — “American Standard Code for Information Interchange” — a code used for storing text characters as binary code.
- **Boolean expression** — A statement that is either True or False, leading to two possible outcomes.
- **branch** — A point in a program where two different options are available to choose from.
- **bug** — An error in a program’s code that makes it behave in an unexpected way.
- **call** — To use a function in a program.
- **comment** — A text note added by a programmer to a program that makes the code easier to understand and is ignored by the program when it runs.
- **condition** — A “True or False” statement used to make a decision in a program. See also *Boolean expression*.
- **constant** — A fixed value that can’t be changed.
- **coordinates** — A pair of numbers that pinpoint an exact location. Usually written as (x, y).
- **data** — Information, such as text, symbols, and numerical values.
- **dictionary** — A collection of data items stored in pairs, such as countries and their capital cities.
- **debug** — To look for and correct errors in a program.
- **encryption** — A way of encoding data so that only certain people can read or access it.
- **event** — Something a computer program can react to, such as a key being pressed or the mouse being clicked.
- **file** — A collection of data stored with a name.
- **flag variable** — A variable that can have two states, such as True and False.
- **float** — A number with a decimal point in it.
- **flowchart** — A diagram that shows a program as a sequence of steps and decisions.
- **function** — Code that carries out a specific task, working like a program within a program. Also called a procedure, subprogram, or subroutine.
- **global variable** — A variable that works throughout every part of a program. See also *local variable*.
- **graphics** — Visual elements on a screen that are not text, such as pictures, icons, and symbols.
- **GUI** — The GUI, or graphical user interface, is the name for the buttons and windows that make up the part of the program you can see and interact with.
- **hack** — An ingenious change to code that makes it do something new or simplifies it. (Also, accessing a computer without permission.)
- **hacker** — A person who breaks into a computer system. “White hat” hackers work for computer security companies and look for problems in order to fix them. “Black hat” hackers break into computer systems to cause harm or to make profit from them.
- **indent** — When a block of code is placed further to the right than the previous block. An indent is usually four spaces. Every line in a particular block of code must be indented by the same amount.
- **index number** — A number given to an item in a list. In Python, the index number of the first item will be 0, the second item 1, and so on.
- **input** — Data that is entered into a computer. Keyboards, mice, and microphones can be used to input data.
- **integer** — A whole number. An integer does not contain a decimal point and is not written as a fraction.
- **interface** — The means by which the user interacts with software or hardware. See GUI.
- **library** — A collection of functions that can be reused in other projects.
- **list** — A collection of items stored in numbered order.
- **local variable** — A variable that works only within a limited part of a program, such as a function. See also global variable.
- **loop** — A part of a program that repeats itself, removing the need to type out the same piece of code multiple times.
- **module** — A package of ready-made code that can be imported into a Python program, making lots of useful functions available.
- **nested loop** — A loop inside another loop.
- **operating system (OS)** — The program that controls everything on a computer, such as Windows, macOS, or Linux.
- **operator** — A symbol that performs a specific function: for example, "+" (addition) or "–" (subtraction).
- **output** — Data that is produced by a computer program and viewed by the user.
- **parameter** — A value given to a function. The value of a parameter is assigned by the line of code that calls the function.
- **pixels** — Tiny dots that make up a digital image.
- **program** — A set of instructions that a computer follows in order to complete a task.
- **programming language** — A language that is used to give instructions to a computer.
- **Python** — A popular programming language created by Guido van Rossum. It is a great language for beginners to learn.
- **random** — A function in a computer program that allows unpredictable outcomes. Useful when creating games.
- **recursion** — Creating a loop by telling a function to call itself.
- **return value** — The variable or data that is passed back after a function has been called (run).
- **run** — The command to make a program start.
- **software** — Programs that run on a computer and control how it works.
- **statement** — The smallest complete instruction a programming language can be broken down into.
- **string** — A series of characters. Strings can contain numbers, letters, or symbols, such as a colon.
- **syntax** — The rules that determine how code must be written in order for it to work properly.
- **toggle** — To switch between two different settings.
- **tuple** — A list of items separated by commas and surrounded by brackets. Tuples are similar to lists, except you can't change them after they've been created.
- **turtle graphics** — A Python module that lets you draw shapes by moving a robotic turtle across the screen.
- **Unicode** — A universal code used by computers to represent thousands of symbols and text characters.
- **variable** — A place to store data that can change in a program, such as the player's score. A variable has a name and a value.
- **widget** — A part of a Tkinter GUI (graphical user interface) that performs a specific function, such as a button or menu.

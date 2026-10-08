
# DRAWING MACHINE

## Creating the String artist

The pseudocode on the previous page plans a function called the String artist, which will turn a string of values into single commands that are sent to the Turtle controller. The next stage is to turn the pseudocode into real Python code, using a function called "split()".

![](img/72d218a7a73c4d4abc7be582ebd85385_145_0.png)

- The "split()" function splits a string into a list of smaller strings. Each break point is marked by a special character ('-' in the program).

This string lists the commands to create the sample house shape

```python
>>> program = 'N-L90-F100-R45-F70-R90-R45-F100-R90-F100'
>>> cmd_list = program.split('-')
>>> cmd_list
```

The "split()" function breaks the string down into a list of separate commands

```python
['N', 'L90', 'F100', 'R45', 'F70', 'R90', 'F70', 'R45', 'F100', 'R90', 'F100']
```

- Write out the pseudocode for the String artist using real Python code. Use the "split()" function to slice up the input string into turtle commands.

```python
def string_artist(program):
    cmd_list = program.split('-')
    for command in cmd_list:
        cmd_len = len(command)
        if cmd_len == 0:
            continue
        cmd_type = command[0]
        num = 0
        if cmd_len > 1:
            num_string = command[1:]
            num = int(num_string)
        print(command, ':', cmd_type, num)
        turtle_controller(cmd_type, num)
```

- This makes the program loop through the list of strings--each item is one command for the turtle

- If the length is 0 (the command is blank), the function skips it and moves to the next one

- Takes the first character of the command (remember, strings start at 0) and sets it as the command type ("F", "U", etc.)

- This takes all the remaining characters from the command by cutting off the first one

- Prints the command on the screen so you can see what the code is doing

- Gets the length of the command

- Converts the characters from strings into numbers

- Checks if the command is followed by more characters (the number)

- Passes the command to the turtle

![](img/72d218a7a73c4d4abc7be582ebd85385_145_1.png)

When the string representing the instructions for the house shape is passed into the String artist, it shows this output in the shell window.

```python
>>> string_artist('N-L90-F100-R45-R90-F70-R45-F100-R90-F100')
N : 0
90 : L 90
100 : F 100
R45 : R 45
70 : F 70
R90 : R 90
R45 : R 45
100 : F 100
R90 : R 90
100 : F 100
```

- Resets the screen and puts the turtle at the center

- The turtle commands are all separated by a "-"

- For command 'F100', the command type is "F" and "num" is "100"

- This makes the turtle turn 45 degrees before drawing the roof

- This command makes the turtle draw the right-hand side of the roof

- The turtle turns 90 degrees, ready to draw the bottom of the house

![](img/72d218a7a73c4d4abc7be582ebd85385_146_0.png)

Each command in the string that is passed to the "string_artist" function is extracted, identified, and executed. A picture of a house is drawn in the turtle graphics window.

## REMEMBER Commands

Here's a reminder of the turtle commands in this program. Some of these are only letter long, while others include a number telling the turtle how far to travel or turn. Each time you activate "string_artist", it adds to the drawing, until "N" clears the screen.

- N = New Drawing
- U/D = Pen Up/Down
- F100 = Forward 100
- B50 = Backwards 50
- R90 = Right turn 90 deg
- L45 = Left turn 45 deg

![](img/72d218a7a73c4d4abc7be582ebd85385_146_1.png)

The program makes the turtle draw a house

## Finish off the code with a user interface

The drawing machine needs an interface to make it easier to use. This will let the user enter a string from the keyboard to tell the machine what to draw.

- This code creates a pop-up window where the user can input instructions. A 'while' loop lets them keep entering new strings.

![](img/72d218a7a73c4d4abc7be582ebd85385_147_0.png)

- The triple quote ("'' tells Python that everything until the next triple quote is part of the same string including the line

```python
instructions = '''Enter a program for the turtle:
F100-R45-U-F100-L45-D-F100-R90-B50
N = New drawing
U/D = Pen Up/Down
F100 = Forward 100
B50 = Backwards 50
R90 = Right turn 90 deg
L45 = Left turn 45 deg'''
```

- Tells the user what letters to use for different commands

End of the string Gets the data needed to create the pop-up window

This line tells the program what to show in pop-up window

```python
screen = screen()
while True:
    t_program = screen.textinput('Drawing Machine', instructions)
    print(t_program)
    if t_program != None or t_program.upper() == 'END':
        break
    string_artist(t_program)
```

- Stops the program if the user types "END" or "Cancel"

- Passes the string to the String function

- This window pops up the turtle window for the user to type a drawing machine string.

```text
Drawing Machine
Enter a program for the turtle:
F100-R45-U-F100-L45-D-F100-R90-B50
N = New drawing
U/D = Pen Up/Down
F100 = Forward 100
B50 = Backwards 50
R90 = Right turn 90 deg
L45 = Left turn 45 deg
```

![](img/72d218a7a73c4d4abc7be582ebd85385_147_1.png)

Turtle control is easier to control, and you don't have to restart the program to draw another picture. Type the program string here and click "OK" to run the program

Drawing machine can be used to create more than just outlines. By lifting the turtle's pen while moving to a new position, it's possible to fill in details. Run the program and try entering the string below

```python
N-L90-F100-R45-F70-R90-F70-R45-F100-R90-F100-B50-U50
```

![](img/72d218a7a73c4d4abc7be582ebd85385_148_0.png)

- Lifts the turtle's pen so it moves without leaving a line
- Puts the pen down to draw window
- The house has window

Time for something different

Now you know how to add details, you can really have fun with the drawing machine. Try drawing this owl using the string of instructions.

```python
N-F100-L90-F200-L90-F50-R60-R60-F30-L120-F30-R60-F40-R90-F30-L90-F30-R90-F30-U90-F40-L120-F40
```

![](img/72d218a7a73c4d4abc7be582ebd85385_148_1.png)

The arrow shows where the turtle stopped. This means the owl's beak was drawn last The string lifts the pen three times to draw the eyes and beak separately

## Achievements

You created the drawing machine program by achieving several targets:

- Used a flowchart to plan a function by working out the decision points and the resulting actions.
- Wrote pseudocode to plan out a function writing out the real code.
- Created the function "turtle_controller" that works out command to execute from the letter and number it is given.
- Created the function "string_artist" that produced a turtle drawing from a string of instructions.
- Made an interface that allows the user to tell the program what to draw from the keyboard.

## Bugs and debugging

Programmers aren’t perfect, and most programs contain errors at first. These errors are known as “bugs” and tracking them down is called “debugging”.

## Types of bugs

Three main types of bugs can turn up in programs—syntax, runtime, and logic errors. Some are quite easy to spot, while others are more difficult, but there are ways of finding and fixing them all.

![](img/72d218a7a73c4d4abc7be582ebd85385_149_0.png)

The Python keyword is "for" not "fir". This will cause an error as no number divided by 0. cannot be less than 5 and greater than 8 at the same time, no free tickets

```python
for i in range(5):
    print(i)
```

```python
a = 0
print(10 / a)
```

```python
if age < 5 and age > 8:
    print('Free ticket!')
```

- Easy to spot: An error is a mistake in the program’s words or symbols, such as misspelled keywords, missing brackets, or incorrect intents.
- Harder to spot: Runtime errors appear only when the program is running. Adding numbers to strings or dividing by 0 can cause them.
- Hardest to spot: Logic errors are mistakes in a program’s thinking. Using "<" instead of ">", example, or adding when you should subtract result in these errors.

## Find and fix a bug

Syntax errors are easy to spot because IDLE highlights them in red when you run the program. Finding runtime and logic errors takes a bit more work.

![](img/72d218a7a73c4d4abc7be582ebd85385_149_1.png)

```python
top_num = 5
total = 0
for n in range(top_num):
    total = total + n
print('Sum of numbers 1 to ', top_num, 'is', total)
```

1 Program: This program aims to add all the numbers from 1 up to the value stored in the variable “top_num”. It then prints the total.

2 Output: The answer for the program should be (1 + 2 + 3 + 4), it shows the answer as “10”. You need to find out why.

# Sum of numbers 1 to 5 is 10

![](img/72d218a7a73c4d4abc7be582ebd85385_149_2.png)

The answer should be “15”, not “10”.

# Looking at the Ghost game through Scratch goggles

Program flow works the same in programming languages. Here are some examples of input, processing, and output in Python’s Ghost game—and what they might look like in Scratch.

# EXPERT TIPS
One script at a time

There’s an important difference between Scratch and Python. In Scratch, lots of scripts can run at the same time. however, the program is made of only one script.

![](bbox=[0.215, 0.243, 0.483, 0.33])

+   Input
In Python, the "input()" function takes an input from the keyboard. It’s similar to the "ask and wait" block in Scratch.

The question in the Scratch block

```
door = input('1, 2 or 3?')
```

"ask and wait" Scratch block

+   Processing
Variables are used to keep track of the score and the function "randint" picks a random door. Different blocks are used to do these things in Scratch.

This Scratch block sets the value of the variable "score" to 0

```
score = 0
```

Sets the variable "score" to 0

```
set score = to 0
```

"set score to 0" Scratch block

```
ghost_door = randint(1, 3)
```

Selects a random whole number between 1 and 3

```
pick random (1) to (3)
```

"pick random" Scratch block

This Scratch block selects a random number

+   Output
The "print()" function is used to output things in Python, while the "say" block does the same thing in Scratch.

Shows a speech bubble containing the words "Ghost game"

Displays "Ghost game" on the screen

```
print('Ghost game')
```

```
say Ghost game
```

"say" Scratch block
# The main loop

This loop tells the story and receives the player's guess. It keeps going on as long as there isn't a ghost behind the door that's picked. When a ghost appears, the "feeling_brave" variable changes to "False" and the loop stops repeating.

```
while feeling_brave:
```

```
  ghost_door = randint(1, 3)
```

```
  print('Three doors ahead...')
```

```
  print('A ghost behind one.')
```

This selects a random number between 1 and 3

```
  print('Which door do you open?')
```

The "print" command displays the text on screen

```
  door = input(1, 2 or 3?)
```

This line asks for the player's

```
  door_num = int(door)
```

# Branching point

The program takes a different path depending on whether or not there is a ghost behind the door that was picked. If there was a ghost, the "feeling_brave" variable is set to "False" if not, the player's score increases by one.

```
if door_num == ghost_door:
```

```
  print('GHOST!')
```

This branch runs if there's a ghost behind the door the player picks

```
  feeling_brave = False
```

```
else:
```

If there's no ghost, the player sees this room.

```
  print('No ghost!')
```

```
  print('You enter the next room.')
```

```
  score = score + 1
```

This shows a message telling the player to run away from the ghost

# Game ending

This runs just once, when you meet the ghost and the loop ends. Python knows this isn't part of the loop because it's indented.

```
print('Run away!')
```

```
print('Game over! You scored', score)
```

The score is a variable—it change depending on how many rooms the player gets through

# REMEMBER

# Achievements

Congratulations—you've created your first Python game! You'll learn more about these commands in the book, but you've already achieved a lot:

Run a program: You've learned to run a Python program.

Structured a program: You've used indents to structure a program.

Used variables: You've used variables to store the score.

Entered a program: You've typed a program into Python and saved it.

Displayed text: You've displayed messages on the screen.

![](bbox=[0.765, 0.825, 0.935, 0.925])
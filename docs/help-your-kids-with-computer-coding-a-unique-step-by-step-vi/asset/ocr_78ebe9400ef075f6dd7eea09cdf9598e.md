# Ghost game

This simple game highlights some of the things to watch out for writing programs in Python. Once the code has been typed in, run the program to play the game. Can you escape the haunted house?

SEE ALSO
Ghost game 98-99 >
doded
Program 100-101 >low

+   IDLE, and use the "File" menu to open a new window. Save the game as "ghost game." Arrange the windows so you can see them, then type this into the code window.

# # Ghost Game

```
from random import randint
```

Use single quotes

```
print('Ghost Game')
feeling_brave = True
```

Only capital letters
where they are shown

```
score = 0
```

Make to add
a colon here

while feeling_brave:

These must be
underscores, not
minus signs

```
ghost_door = randint(1, 3)
print('Three doors ahead...')
print('A ghost behind one.')
print('Which door do you open?')
door = input('1, 2, or 3?')
door_num = int(door)
```

This section needs to be
ented by four spaces.
If this doesn't happen
automatically, check that
there is a colon after
"feeling_brave"

Use two equals
signs here

```
if door_num == ghost_door:
print('GHOST!')
feeling_brave = False
else:
print('No ghost!')
print('You enter the next room.')
score = score + 1
```

This indent will start
at eight spaces and
needs to be reduced
to just four spaces

```
print('Run away!')
print('Game over! You scored_')
```

Delete all
idents here

There should be no quotes
around 'score' here

![](bbox=[0.735, 0.264, 0.815, 0.344])

![](bbox=[0.45, 0.852, 0.185, 0.988])

![](bbox=[0.65, 0.328, 0.735, 0.388])
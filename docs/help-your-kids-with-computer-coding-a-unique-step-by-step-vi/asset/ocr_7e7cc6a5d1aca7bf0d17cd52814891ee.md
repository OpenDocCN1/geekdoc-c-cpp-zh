When the string representing the instructions for the house shape is passed into the String artist, it shows this output in the shell window.

```
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

Resets the screen and puts the turtle at the center

The turtle commands are all separated by a "-"

For command 'F100', the command type is "F" and "num" is "100"

This makes the turtle turn 45 degrees before drawing the roof

This command makes the turtle draw the right-hand side of the roof

The turtle turns 90 degrees, ready to draw the bottom of the house

![](bbox=[0.535, 0.215, 0.95, 0.545])

Each command in the string that is passed to the "string_artist" function is extracted, identified, and executed. A picture of a house is drawn in the turtle graphics window.

# REMEMBER Commands

Here's a reminder of the turtle commands in this program. Some of these are only letter long, while others include a number telling the turtle how far to travel or turn. Each time you activate "string_artist", it adds to the drawing, until "N" clears the screen.

+   - N = New Drawing
- U/D = Pen Up/Down
- F100 = Forward 100
- B50 = Backwards 50
- R90 = Right turn 90 deg
- L45 = Left turn 45 deg

![](bbox=[0.175, 0.585, 0.58, 0.935])

The program makes the turtle draw a house
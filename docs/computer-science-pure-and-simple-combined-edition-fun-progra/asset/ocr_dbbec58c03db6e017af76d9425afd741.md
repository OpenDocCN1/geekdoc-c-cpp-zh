# # #19 ENHANCED WANDERING TURTLE SOLUTIONS

EXERCISE 5
to wander :stepSize :dizziness

```
; turn right by a random amount could be negative
; turn right by a random amount up to dizziness
right difference :dizziness quotient: :dizziness 2
n; move forward by stepSize, repeat twice
repeat 2 :stepSize wait 1
```

end

# #21 MAZE II: WIN OR LOSE?

A basic maze
Create a button labeled "go." Draw a maze using thick
lines from the Drawing Center (under the paintbrush icon). Be
sure the color you are using is labeled 15; please your mouse
over the color in the Drawing Center to be.

to Main
talko "t1"
launch [repeat 2000 [forward 3 direct leadcar || ]
waituntil [colorunder = 15]
announce [You lose!]
reset
end

```
to direct key
if (ascii:key) = 28 [set 270 fd 1]
if (ascii:key) = 29 [set 90 fd 1]
if (ascii:key) = 30 [set 0 fd 1]
if (ascii:key) = 31 [set 180 fd 1]
if (ascii:key) = 37 [set 270 fd 1]
if (ascii:key) = 39 [set 90 fd 1]
if (ascii:key) = 38 [set 0 fd 1]
if (ascii:key) = 40 [set 180 fd 1]
if (key = "s") [stopall]
```

end

to go
Main
talko "t1"
setpos [-319 -164]
set 0
end

# EXERCISES:

+   1. Use the turtle-hatching button to place a new turtle at the
destination point in the maze. This is t2.
2. Underline line, and add a shape dog to your Shape Center
 you have Micro Worlds EX.

to Main
talko "t1"
launch [repeat 2000 [forward 3 direct leadcar || ]
when [touching :"t2" [set "dog" ]]
waituntil [colorunder = 15]
announce [You lose!]
reset
end

Flow chart addition:

![](bbox=[0.562, 0.213, 0.935, 0.713])

3. In MicroWorlds, you will need to build a castle and a cloud
to your Shape Center from the Drawing Center list of single
shapes (in the Paint/Clip window under the flower icon).
Click on the button and then on T2 to change its shape to a castle.

Turtle 1 changes to shapes when he hits the castle:
Add some shapes to the first 9 blanks in your Shapes Center.
This is so we change shapes using random 10, and get a
random choice of those 9 shapes.

194
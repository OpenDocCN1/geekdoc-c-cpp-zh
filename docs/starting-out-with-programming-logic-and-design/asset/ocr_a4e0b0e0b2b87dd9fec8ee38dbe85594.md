# Nested Loops

CONCEPT: A loop that is inside another loop is called a nested loop.

A nested loop is a loop that is inside another loop. A clock is a good example of something works like a nested loop. The second hand, minute hand, and hour all spin around the face of the clock. The hour hand, however, only makes 1 revolution for every 12 of the minute hand's revolutions. And it takes 60 revolutions of the second hand for the minute hand to make 1 revolution. This means that for every complete revolution of the hour hand, the second hand has revolved 720 times. Here is pseudocode with a loop that partially simulates a digital clock. It displays the seconds from 0 to 59

```
Declare Integer seconds
For seconds = 0 To 59
  Display seconds
End For
```

We can add minutes variable and nest the loop above inside another loop that cycles through 60 minutes:

```
Declare Integer minutes, seconds
For minutes = 0 To 59
  For seconds = 0 To 59
    Display minutes, ":", seconds
  End For
End For
```

To make the simulated clock complete, another variable and loop can be added to count the hours:

```
Declare Integer hours, minutes, seconds
For hours = 0 To 23
  For minutes = 0 To 59
    For seconds = 0 To 59
      Display hours, ":", minutes, ":", seconds
    End For
  End For
End For
```

If this were a real program, its output would be:

```
0:0:0
0:0:1
0:0:2
```

(The program will count through each second of 24 hours.)
23:59:59

The innermost loop will iterate 60 times for each iteration of the outermost loop. The middle loop will iterate 60 times for each iteration of the outermost loop. When the outermost loop will have iterated 24 times, the middle loop will have iterated 1,440 times and the innermost loop will have iterated 86,400 times! Figure 5-21 shows a flowchart for the complete clock simulation program previously shown.
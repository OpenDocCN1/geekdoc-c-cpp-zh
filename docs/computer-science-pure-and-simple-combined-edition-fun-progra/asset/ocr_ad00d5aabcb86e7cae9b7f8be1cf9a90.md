# #5 Simple Logo House

Let's work on drawing using Logo. Open up Square (not Square1 from last time). Square should look like this:

```
to Main
cc
talkto "t1"
;works with turtle named t1
repeat 20 [Square]
end

to square
:draws a square of 50 units
pd
repeat 4 [forward 50 right 90 wait 1]
end

to Start
Main
end
```

Save it as House. This makes a copy of it that we will change.

So far we have only been drawing a square or a line. Let's do some experimenting to see if we can draw a triangle. Go to the Command Center and type ce <center>, to clear the command center, then eg <center> to clear the graphics.

First, let's talk about Degrees. Degrees measure how much you are turning. When the turtle draws a square, it makes 90-degree turns. So a 90-degree turn is the measure of a right angle. But how much is a degree, anyway? In the Command Center, let's tell our turtle to put its pen down, turn one degree, go forward 50 and back 50.
Here’s mine:

```
local "originalY
make "originalY ycor
sety sum ycor 50
wait 1
sety :originalY
```

We can now make a few more adjustments.
It is common to want to re-write a procedure on a trial basis, but you don't want to lose the old one, at least not yet. Here is what I do: I rename the existing procedure to say, doJumpOld and write the new procedure as doJump. That way you do not have to search through your program to change all the calls to doJump. They stay as they are, only now they are calling your new version of doJump. Then, when we're sure we've made a good change, we can get rid of doJumpOld.
Here is my doJumpOld:

```
to doJumpOld :height
seth 0
forward :height
: wait 1
back :height
seth 90
end
```

Make a new doJump on your procedures page. with the same first line as before. Add our code snippet from above, which allows us to:

+   * create a new pigeonhole (using local) and save the y coordinate (using ycor) of the first position
* move the turtle to a location where we have added the value stored in height to the y coordinate
* pull the y coordinate of the first position from its pigeonhole
* move the turtle back to that.

Again, write down what you think before you look at what I came up with on the next page!
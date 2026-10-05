This was just to give you a brief idea about processes. Let's go back to Version 1. Take the call to jump out of Main.

# Jump has a bug!

We need a new procedure jump which will be called when the button is clicked. Add this procedure to your Procedures Page:

```
to jump
dojoump 20
end
```

This gives us a way to pass a number to doJump. Now try your program. Well, it is fun. You can make the dog walk along and then, by clicking on jump, make him a little jump and then carry on. this way we have to get the label we want on the button and we will keep the program out where we can see it in the Procedures Page.

Did you notice something odd? Did you notice that the dog kept getting higher and higher after we click jump? It didn't seem to come all the way back down after a jump.

Well, folks, we have a bug in our program. Nothing is not right, and we need to debug our program. That is, we need to find what the error is. To debug a program, the first step is to find out what is causing the problem. When the turtle walks, it does not move higher.

Try stopping the walk (by clicking again on the Start button) and clicking on the jump button. Jump seems to work fine and walk seems to work fine when they are run separately. But when both processes are running at the same time, we seem to have a bug in our program!

So, it only occurs when both processes are running at the same time. I would like to see the movement with the shape of the dog obscuring the turtle. In Main, put a semicolon in front of the setsh line, like this:

```
; setsh [dog1 dog2]
```

The computer sees a line with a semicolon and considers it a comment, not part of the program. It is like all the words to the right of the semi-colon are invisible to Logo and visible to humans. We have just made this line invisible to Logo. (We "commented the line out.") Programmers do it all the time)

Let's turn the dog back into a turtle. Type a command in the Command Center: setsh 0 <center>. Now run the program. Seeing it this, with the naked turtle, makes me a little suspicious of what is happening with forward. Sometimes the turtle points out, sometimes it left.

Let's take a hard look at our two processes and try to figure out what happens that is different, when both processes are running at the same time.

You can see that both walk and doJump tell the turtle to move forward. Forward just means "go in the direction your head is pointing." So, if the doJump process is running, then the head is pointed up (setsh 0). So during the time the doJump process is running, the walk process actually
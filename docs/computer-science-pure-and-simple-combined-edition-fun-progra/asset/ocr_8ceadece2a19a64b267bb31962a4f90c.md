First, let's consider what code we will use to make our loop. We will have a bunch of steps, and at the end of the steps, we will get input from the user on whether to loop or not. We could pattern our loop after Hangman loop, using forever to start it, and stopping it with an if statement at the end. For example, we can ask the user if he wants to continue, or N.

```
;if the answer is N, wait a while, and stop the semicolon.
```

Notice that it is not Logo, but pseudocode, so we put it in front of it.
Here's another way to do it: don't use forever at the top; just start the steps in the loop. Then at the end of the loop, ask the user if he wants to continue, or N. If the answer is Y, we call Main. If it is N, we don't. So we are calling Main from within Main. Sound strange? It works, as long as you have a get out of the loop. The problem here is that the first line of our Main is setup, but we don't want to run setup every time we go through the loop. We would have to move out of Main and into the Start button procedure. So Start would look like this:

```
Start
c
setup
Main
end
```

The advantage of this plan is that we don't have to stop all the action until the user presses the Start button or closes the window. We could add a stopall button too.

So, which loop shall we use? Let's use the one that calls Main from Main. We could use practice with that one. Now our flow chart for Main looks a little different at the top:

![](bbox=[0.398, 0.005562999999999999, 0.503, 0.638])

Next, let's brush up on variables a little. Remember that variables are storage places, like pigeonhole mailboxes. A first line for a procedure can create a storage place, like this:

```
to house size
```

Here house is the name of the procedure, and size is the name of the variable used inside the procedure. So, now the procedure house needs one input. When we call this procedure house from Main, we need to send it an input to go into the variable size. So our command from Main would look like this:

```
house 1
```

for the full-sized house, or

```
house 0.5
```
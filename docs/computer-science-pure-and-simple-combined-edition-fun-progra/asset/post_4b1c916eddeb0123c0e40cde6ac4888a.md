
The walk procedure, you can see that we added an input to forward—the value in the variable stepsize. That value is passed from Main when the procedure walk is called, which now has an input. See how they are tied together?

![](img/242aaa06c3a3208f16d97cdd92303648_58_0.png)

Go to your Graphics Page and click on the Start button. How did it go?

My dog went backwards! Yours may be going up or down! We forgot to set the heading of the turtle/dog before we called walk. (Remember, the heading is the direction the turtle is facing.) My dog faces the opposite direction from my horse. We forgot one of our programming goals, which I repeat here:

It must work every time for every one. In other words it can't depend on the user doing things in the right order, or depend on the turtle facing the right direction or some other condition. It must account for and handle all those possibilities itself.

How can we do that? We'd like to point the turtle to the left, no matter what it was doing before. So we need to set the heading, using seth, pronounced set-H for set heading. Let's try this: Add seth–90, or seth 270 (same thing) to Main. (Do you wonder where these numbers come from? Take out a compass and look at the numbers around the rim. They add up to 360, the number of degrees in a circle. North is 0, or 270 is west. Or in our case, to the left.)

We are pointing the turtle's head to the left, no matter what it was doing before that.

```
to Main
cg
ecc
pu
talkto "t1"
setsh [dog1 dog2]
seth 270
repeat 200
[walk 5]
```

We want our **walk** to be able to work with any shapes in any direction. That is why we wouldn't add **seth 270** to the walk procedure itself. It also makes sense to put it before the **repeat**, because it would be inefficient to call it 200 times. I find the dog a little slow, so let's try increasing the step size to 10. Change **Main** and run your program again.

```
to Main
cg
ecc
pu
talkto "t1"
setsh [dog1 dog2]
seth 270
repeat 200
[walk 10]
```

There, I think that looks pretty good. Now let's do **jump**.

# The jump procedure

Well, I guess the obvious variable in a **jump** procedure would be "How high?" or height. So let's get started:

```
to jump :height
seth 0
forward :height
wait 1
back :height
```

What do you think of this procedure? Do you think it will work? Let's add it to **Main** and give it a try. Here is the new **Main:**

```
to Main
cg
cc
pu
talkto "t1
setsh [dog1 dog2]
seth 270
repeat 200
[walk 10
jump 10]
end
```

Give your program a try.
My dog just kept going up!

Do you see why? In jump, we set the heading of the turtle to up (seth 0) but we never set it back again! In other words our jump procedure had the unpleasant side effect of changing the direction the turtle was headed. But how do we set it back to its original direction when it is finished jumping? Let's see the heading back to 270 (to the left) when it is finished jumping.

```
to jump :height
seth 0
forward :height
wait 1
back :height
seth 270
end
```

Do you see how that works? Now try it.
I would like the dog to walk further before it jumps. How do we do that?
Let's try changing the size of the steps by changing Main as follows:

```
repeat 200
[walk 100
jump 10]
```

Well, the result is interesting, but the animation doesn't seem to work! What went wrong? Let's take another look at our walk procedure. Here it is again:

```
to walk :stepsize
repeat 2
[forward :stepsize
wait 1]
end
```

What is happening the dog is walking along, changing shapes once and then jumping. In order to get it to walk more than it jumped we made the stepsize larger (100). But this ruined the animation because I am not calling forward very often. What I really want is for the dog to walk along many steps while changing, and to jump. We need to revise our walk procedure so that we can control both the step size and the quantity of steps. Let's add another parameter (variable) to our walk procedure.

```
to walk :stepsize :qsteps
  repeat :qsteps
    [forward :stepsize
      wait 1]
end
```

Qsteps stands for quantity of steps. Now we can easily control the size of each step and the quantity of steps with each call to walk. Change Main to make use of this new power and try your program.

# to Main

```
cg
cc
pu
talkto "t1"
setsh [dog1 dog2]
seth 270
  repeat 200
    [walk 10 10
      jump 10]
end
```

There, that's pretty good! Change both inputs to walk. What happens? Change the input to jump. What happens?

The method we used to develop these procedures should show you that finished projects start out as finished projects. You need to try things, adapt them to make them better and sometimes abandon them if you find a better way to accomplish a task.

When you see someone's finished project, don't forget that all projects start out the same way, a blank page. It just takes time and a large amount of perseverance to make them into masterpieces.

# Save your work

Be sure to save your work as Walk.

We now have three movement procedures, but we are not really using the square procedure at this point. So let's delete it.

Here is the complete procedures page:

```
============================
to Main
cg
cc
pu
talkto "t1
setsh [dog1 dog2]
seth 270
repeat 200
[walk 10 10]
end
============================
to jump :height
seth 0
forward :height
wait 1
back :height
seth 270
end

to Start
  Main
end

to walk :stepsize :qsteps
  repeat :qsteps
    [forward :stepsize
    wait 1]
end
```

Exercises:
1. Make a file called Buzz.
2. Make the label be jump.
3. Put the button on the Graphics Page.
4. Save your work.
5. Make the button be called Buzz.
6. Extra credit: Make the dog like this (img/242aaa06c3a3208f16d97cdd92303648_63_0.png)

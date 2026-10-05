# #11 Do the Logo Walk

Now, let's do some more animation. I would like to develop a procedure called walk.
From the file menu, open your project saved from an earlier lesson called Square1. Then from the file menu select "Save Project As" and save your project as Walk. Remember, this is the project where a horse was trotting in invisible squares. On the Procedures Page, your program should look like this:

```
to Main
  cg
  cc
  pu
  talkto "t1"
  setsh [horse1 horse2 horse3]
  repeat 20
    [square 30]
end
```

```
to square :length
  repeat 4
    [forward :length right 90 wait 1]
end
```

```
to Start
  Main
end
```

# Our approach

We are going to experiment with making a procedure walk. We will start out with a general idea of what we want to do but we will build the procedure bit by bit as we see what works and what doesn't. And we will make mistakes along the way that we will learn from and use to make our procedure better.

After we do walk, I would like to do jump. Eventually, I would like to make a critter walk along and jump over things.
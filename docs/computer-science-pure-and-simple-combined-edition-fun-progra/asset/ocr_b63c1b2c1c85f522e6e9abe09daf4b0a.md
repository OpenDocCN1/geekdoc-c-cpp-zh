```
Main
cc
talkto "t2
setsh [dog1 dog2]
seth 270
launch [repeat 200 [walk 10 10] ]
talkto "t3
setsh [skater1 skater2 skater3]
seth 90
launch [repeat 200 [walk 10 10] ]
end
```

There! Pretty cool, eh! Be sure to save your work. This program launches two processes that operate independently.

# Exercise your skills

Learning how to program is a bit like learning to ride a bike. Your teacher can tell you how to do it; others can show you how to do it; and you can read about it. But there is only one way to learn and how that is to do it. You have learned quite a few built-in procedures and some programming techniques. You should consolidate your knowledge by actually putting these things to use.

+   1. Save your file under jump2. Now save it as tornado.
2. Modify the file so as to make the following things happen at the same time as the dog running and jumping the skater:
    * Place another turtle, t4, in the shape of a castle in the lower right corner of the picture.
    * Yet another turtle, t5, takes the shapes of tornado1 and tornado2, and moves to the right towards the castle.
    * Spray-paint some turquoise blue (cyan) near the castle. When it strikes the blue, the tornado jumps over the castle.
    * When the tornado jumps, the castle turns into a cloud and then back into a castle.
3. In a new file, draw a maze with the drawing palette, using blue lines. Using the same idea as colorGrayHit, set up a turtle proceeding through your maze. Start with a start button. You may want to use the procedure random, which delivers a random number. Random 100, for example, returns a number between 0 and 99.
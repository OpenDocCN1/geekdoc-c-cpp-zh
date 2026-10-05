
In MicroWorlds EX, we can give the button a label and an instruction. As a rule, let's make these the same thing. Put Start in both places, where it says "nothing" in the picture above.

Click OK. Then drag the button so it is nice and tight in the bottom left corner of the Graphics Page.

I suggest you save your work often. On a PC, if you press the two keys Ctrl and S together, you will have the revised project under the name you just gave, Square.

Now click on the Start button. We get the error message "I don't know how to Start." This is exactly what we are going to teach MicroWorlds now! How are we going to teach it? You guessed it, we will create a procedure Start.

Go back to the Procedures Page. Remember how? Now, to add the word Start to MicroWorlds' vocabulary, we need to make a Start procedure.

First I would like to comment on program design. Remember these lessons are to teach you good programming techniques. They are not just to teach you about MicroWorlds or Logo. The computer language C is a favorite professional language, and so is C++. Both of these languages, in particular C++, have been designed to help programmers manage the complexity of computer programs. Both of these languages start every program's execution at a procedure named Main. This means that the first procedure to run is always called Main. If you are reading a program in C or C++, you would typically start by looking for the procedure named Main. I feel it is a very good convention to follow.

So we will make a Start procedure which will call (run) our Main procedure. Add these to your procedures:

```
to Start
Main
end

to Main
cc
talkto "t1"
;works with turtle named t1
repeat 20 [Square]
end
```

Notice our new instruction, talkto "t1". This makes sure we are addressing the first turtle, t1, and not some other turtle. Save your work by striking <ctrl> and s.

We now have a complete program! Main tells the computer what to do first, then next, and so on. The procedures listed after Main tell the computer how to do the commands it doesn't know already.

The first instruction in Main tells MicroWorlds to clear the Command Center. This is so we know that any error messages we see are new ones. The next instruction in Main tells MicroWorlds which turtle should perform the actions in the following instructions. It is not necessary to have that instruction if there is only one turtle, but it improves the readability of our program, which is one of our goals.

The third line uses the built-in repeat which requires two inputs: a number and a list of instructions to repeat. We only have one instruction, so to make it a list you just put square brackets around it. We will be talking about lists later.

Try running your program by going to the Graphics Page and clicking your Start button. Now try running it in Presentation Mode by going to the View menu and clicking on Presentation Mode. Then click the Start button. To get out of Presentation Mode, double-click on the black border.

One bit of house cleaning to do. As this and other programs grow, your Procedures Page gets very large. So do not waste time for procedures, you should keep them in alphabetical order. To move around, highlight the whole procedure by putting the mouse button down above it, holding it, and moving the cursor to the other side. Now go to the Edit menu, and select cut. The lines seem to vanish. Really you have them on an invisible clipboard. Now move the cursor where you want the lines to be, and from the Edit menu select paste. Presto, they show up in the new spot! This cut and paste routine works in nearly all computer applications. You can also use copy and paste if you want to make copies.

I usually do something special with Main to make it particularly easy to find, such as type double lines before and after it. By the way, MicroWorlds is not case-sensitive, so it doesn't matter if you type capital or lower-case letters. Here is my Procedures Page:

```
to Main

cc
talkto "t1"
;works with turtle named t1
repeat 20 [Square]
end

to square
;draws a square of 50 units
p
forward 50 right 90 wait 1
forward 50 right 90 wait 1
forward 50 right 90 wait 1
forward 50 right 90 wait 1
end

to Start

Main
end
```

Can you figure out how to rewrite your **square** procedure using **repeat**? Remember **repeat** needs two inputs, a number indicating how many repetitions, and a list of instructions to repeat—with brackets around it [like this].

So that you can continue with this project at another time, please save your work under its current name, **Square**, by striking \<ctrl> and s. **Run** your program (by clicking on the Start button) for a teacher, and **show** you have proper format on the Procedures Page.

An assignment: Let's play with it.

- Repeat the instruction in **square** three rather than four times. Press **Start** repeatedly. What happens?
- Make larger squares.
- Wait longer.
- Try a different angle and see what you draw. This means change the input to **right**. For example, **right 34** instead of **right 90**.

(After you make these changes, save it under a different name, such as **mysquare**. We will be pulling up **Square** later and want it to be a clean copy.)

## #3: Introduction to Animations

Let's review the Shape Center.

First, we find the Drawing Center. Locate the paintbrush icon at the top, Click on it.

![](img/242aaa06c3a3208f16d97cdd92303648_22_0.png)

Look at the icons at the top:

![](img/242aaa06c3a3208f16d97cdd92303648_22_1.png)

The landscape picture allows us to choose a background. The flower icon window contains shapes, and the walking-people icon window contains shapes just for animations. Click on the walking-people animations icon.

![](img/242aaa06c3a3208f16d97cdd92303648_22_2.png)

These shapes are for the turtle to “wear.” But first we have to install them into the Shape Center. Click on the blue band at the top of this shape window, and hold it down. Move the window to the left. Now, at the bottom of the page on the right, find the folder tab that says “shapes.” Click on so that it’s the folder that shows. It should look like a grid of dots.

Make sure your window full of possible shapes is next to the Shape Center full of empty dots.

![](img/242aaa06c3a3208f16d97cdd92303648_23_0.png)

Now, let’s drag some shapes over from the Painting/Clipart window on the left to the Shape Center on the right. After we install shapes like this, they have a name and number and are usable as “clothes” by the turtle.

![](img/242aaa06c3a3208f16d97cdd92303648_24_0.png)

Pause your mouse arrow over one of the installed shapes, and you will see its name, number, and size in pixels. We can get rid of the Painting/Clipart window by clicking on the red x in the upper right.

Click on one of the shapes in the Shape Center, and then click on the turtle. Presto! it's wearing the shape.

You can hatch more turtles, click a shape, and click the turtle. Make the shape smaller or larger by clicking first on the magnifier icon and then on the shape. Drag the turtles around.

## Getting Started

Open a new file. For now we will use horse1, horse2, horse3. Go ahead and install your horse shapes to the Shape Center, and hatch a turtle.

We'll use the command setsh, for set shape. We give the computer set list of shapes. Every time the computer calls forward, the computer comes back to the shapes list and tells the turtle to change shapes to the next shape. Let's set our shapes. Type this in the Command Center:

```
setsh [horse1 horse2 horse3]
```

Press <enter>. We're ready to go! Now let's get our turtle started walking.

Type this into the Command Center: fd 1 . Execute it by pressing <enter> at the end.

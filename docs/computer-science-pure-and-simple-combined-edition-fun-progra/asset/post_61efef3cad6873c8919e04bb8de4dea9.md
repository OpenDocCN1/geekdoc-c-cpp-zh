
When the house program is working properly, **show** your teacher. Save your work using <ctrl> under the name you already gave it.

## Skyscraper project assignment:

We are going to make some “code” in English to start with. Take your drawing of a big building. Put measurements on it, like we did on our house drawing. Now, make some instructions in English for drawing it. Make a Main procedure that describes how to draw the building in just a few lines in English. (For example: draw the outline, move the turtle, draw the door, move the turtle, draw a window, move the turtle ... Then for each of those lines, make a procedure that says in detail how to follow the step in English. Remember, our goals call for procedures that have one purpose only.

## #7 Logo Skyscraper Project 1

Now it is time to draw the big skyscraper!

If you have done your assignments, you have made a careful drawing of a skyscraper designed by you. You have a list of how to do it, in English. Now you need to translate to Logo.

You already have the tools you need to do this, except for the concept of a row of windows. To make a row of windows, create a procedure called **windowrow**. In it, use the **repeat** command to repeatedly draw a window plus the space between it and the next window. For instance, **window and window** could look like this:

```
to window
set 0
pd
repeat 4 [forward 5 right 90]
end
```

```
to windowrow
repeat 15 [pd window seth 90 pu forward 10]
end
```

Start a new file for this project. You can name it MyBuilding. Write your main procedure first. This will serve as a list of procedures that you will create, for example:

```
to Main
cg
movedown
outline
move1
door
move2
windowrow
end
```

Now you need to write the first of these procedures and test it. You can do this in the Command Center, where you can watch the turtle moving as you type in commands. First create a set of commands that draws your outline. Then highlight them, **copy** them using the **edit** menu, and **paste** them on the Procedures Page. Add a procedure name, "to," and "end."

For example, your **outline** procedure in the Command Center might look like this:

```
set 0
pd
repeat 2 [forward 150 right 90 forward 50 right 90]
pu
```

So you highlight all of them and copy them to the Procedures Page. Put “to outline” at the top, and “end” at the bottom, and you have a procedure. You can call the procedure from the Command Center by typing its name. Remember to make procedures that do one thing (draw an outline) not two (such as move to a spot and draw an outline). Add a comment (starting with ";") to each procedure telling it what it does. Test it by typing outline in the Command Center and pressing <enter>.

Now write the next procedure, test it, and so on. Look for chances to use the built-in procedure repeat, which can repeat any procedure that you write. Also, don’t forget pd and pu as you move the turtle around.

As you work, remember our goals for programming with style:

1. Set up the plan of attack ahead of time.
2. Use small, one-purpose-only procedures whenever possible. This makes it easy for someone to change it later.
3. Document your work so the next person can understand it.
4. The code must work every time for every one.
5. Choose consistent, sensible names for procedures.

## #8 Logo Skyscraper Project 2

Improve your building. Add at least three more items: steps, porches, and decorative columns on the corners, for example. See the troubleshooting guide in the appendix if you need to. You can color your building using programming commands such as pu, fd 3, setc 15, and fill. Add a Start button.

## Skyscraper Project Requirements

Requirements:

- Your program works.
- Your building must have an outline plus at least three different features (window, door, antenna). It must also have three enhancements, such as steps, porches, or columns. Color using programming commands is extra credit. (Extra credit items are not extra for high school students).
- Procedures do one thing (draw a window or move to another spot, but not both).
- Each procedure contains a comment, for example, “;moves up and over to the next position.”
- Main is set off by double lines. Other procedures are in alphabetical order.
- For extra credit, create a program that makes an enhancement to a cityscape, such as a bridge, a newsstand, or a tree.

Make sure your project meets these requirements, and hand it in to your teacher for evaluation against the requirements.

## #9 Logo Variables

Now we are going to pick up our Logo programming again. If we want to draw a building, like before, but this time we want to be able to tell the computer to draw it twice as big? Or half as big? We will be able to do this easily we figure out how to use *variables*. These are values, like the height of the building, that can vary, or change, but at the same time are represented with just one name. *Height* is an example of a variable name.

## Let's talk variables

When you start a program, such as MicroWorlds, Word or Excel, you usually double-click on an icon. This is an instruction to the operating system to look on the hard drive and find the program that is associated with the icon. When the operating system finds it, the operating system reads it into working memory (also loading it) and executes or 'runs' the program. This is why, in the PC world, files that run usually end with ".exe" for execute. Working memory is the place where programs are temporarily stored and where they live as they are running. This is the RAM that you buy when you buy your computer. In it there are millions of places, each with an address, where we and as programmers, can store things.

![](img/242aaa06c3a3208f16d97cdd92303648_43_0.png)

Imagine the working memory contains a bunch of pigeonholes, like mailboxes in a post office. To use one of these storage places, here's what we have to do: we need to reserve the spot and name it. Let's pick one and give it a name—how about "Gus"? Then we can use Gus to hold a number, word or list. Suppose we want to use or change what's in the mailbox. Since we have named the mailbox, we can tell the computer where to find it. So, how do we go about reserving and naming the spot? MicroWorlds has some built-in procedures and operators to assist us. Here is one:

**Local** reserves and names a storage place. Let's set up a test program to investigate using *local*.

## Test program

Open MicroWorlds, and open a new project. You can name it **Test** and save it.

Now we will make a little procedure to use variables. We'll call our first variable Var1. We want to reserve and name our variable (storage place) using *local*.

| | | | | | |
|---|---|---|---|---|---|
| | | | | Var1 | |

## Mailbox Named Var1

Let's make a procedure called TestVar, for test variables. Type the following procedure on the Procedures Page:
to TestVar
local Var1; reserves and names a storage space
show "Var1;we want to print the value in the storage space
end

Var is just a command that prints the item out in the Command Center, so we can see what the computer is thinking.
OK, so does it work? Test it by typing TestVar in the Command Center.
Hmm, something does print there! But what is going on?

Let's set up a Start button. Make the button, label it Start, and on the Procedures Page add this:
to Start
Main
end

Also make a Main:
to Main
TestVar
end

Go back to your Graphics Page 1 and click on the Start button. In the Command Center you will see the computer print:
Var1

Oops! This procedure is the name of the variable (mailbox), not what is in the mailbox (a number).
The built-in procedure local is a procedure with one input—the name of the variable, in this case Var1. Local tells MicroWorlds to reserve a spot in memory to store things in, and it tells MicroWorlds that we will name this spot Var1. The spot is a little mailbox with an address of Var1.
As always, it helps to view the jigsaw puzzles, which show that local uses Var1 for an input:

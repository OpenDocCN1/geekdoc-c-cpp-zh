
![](img/7ea6f60bb53ecc17dd8979f66d5502d6_14_0.png)

*Figure 2-3. Opening the Minecraft file with WinRAR*

First, you want to go into the folder "bin" and then right click on the file "minecraft", or "minecraft.jar" if you have extensions on. This is where our archiving software is used. As I have WinRAR, these options appear when I right click the file (Figure 2-3).

Click "open with..." and then whatever archiving software you use. Now go to wherever your downloads folder is, and double click the "forge" folder. Highlight everything in the forge folder, and simply drag it across into the Minecraft folder.

Close the two windows and run Minecraft to make sure everything still works. We have nearly finished installing the mod, as all we need to do is head back into our .minecraft folder, and right click on any empty space in the window, and click the "new folder" button, and call it "mods". Simply copy or move the computercraft folder you downloaded, into the "mods" folder we just created and you're done! Sometimes you will find that there is already a "mods" folder in which case you will not need to create one.

## The ComputerCraft Command Line

Now that you have installed ComputerCraft, the first thing you will want to do is to make your first computer—Figure 2-4 shows a normal computer and Figure 2-5 an advanced computer. You can use either for the examples in this book.

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_15_0.png)

*Figure 2-4. The Computer recipe*

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_15_1.png)

*Figure 2-5. The Advanced Computer recipe*

After right clicking on your new computer, we can begin. First, we need to learn how to navigate through the computer itself. It works with "directories"; everything is in a directory, and we need to learn how to use them. To see what is in your current directory, type in "ls" (list) or "dir" (directory).

Both commands do exactly the same thing. The command "ls" is what people in the Linux world do to list the contents of a directory, and "dir" is the same command, harking back to the days of Microsoft DOS and the Windows command line.

You should see something like Figure 2-6.

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_16_0.png)

*Figure 2-6. The Computer Command Line*

The only thing in our directory is another directory, "rom." To tell the difference between programs and directories instantly, I recommend using advanced computers; although more expensive, they come equipped with more handy tools than standard computers, including colour-coding. It displays directories as green, and programs as white.

To move into our "rom" directory, we type in "cd rom", and then press Enter. The command "cd" stands for "change directory". After typing "cd rom" (no pun intended), type the "ls" or "dir" command to see what's in there (Figure 2-7).

Now things are getting interesting. We now have four options: apis, programs, startup and help. If we "cd" into "programs" we are greeted with a whole host of assorted programs, including apis. To find out more about any program, simply type in "help" and then the name of the program. There is some pretty interesting stuff in there, so I recommend you look through it all.

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_16_1.png)

*Figure 2-7. Commands*

Now we want to get back to our main directory. To go up a level, as it were, type in cd ..; to make your own directory, enter the command mkdir, and then the name of your new directory.

It's a good idea to create a directory in which to keep all your stuff, including the example projects that you will make as you work through the book.

Create this in the root directory above rom. If you are currently in the rom directory, type:

```
cd ..
```

To move up to that directory and then type:

```
mkdir mystuff
cd mystuff
```

See Figure 2-8.

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_17_0.png)

*Figure 2-8. Creating a directory for your stuff*

### The Lua Command Line

To enter a solely Lua command line, type lua into the command line. From now on, all the commands that you type into the command line will be assumed to be in the Lua programming language.

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_18_0.png)

*Figure 2-9. Arithmetic in the Lua Command Line*

So in this example, we have typed the command

```lua
print(2 + 2)
```

...into Lua and it has told us the answer 4.

In Chapter 3, we will return to the Lua command line as we learn more about how to make use of this powerful programming language.

### The Lua Editor

Although the Lua command line is great for experimenting while we learn the language, it does not remember the commands that we type in. To do that we need to use an editor that will allow us to create and edit files containing Lua programs that we can run, print or transfer to floppy disk to move them from computer to computer.

To make a program, simply type edit, and then the name of your program. You will be brought to a screen that looks like Figure 2-10.

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_18_1.png)

*Figure 2-10. The Lua editor*

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_19_0.png)

*Figure 2-11. The Lua options*

This is the place you will invariably write your hundreds of useful programs, but first let's take a closer look at it. In the bottom right-hand corner, we can see which line we are on. The bottom left-hand corner tells us to press Control to see the access menu (Figure 2-11). After you press the Control key (don't hold), we are presented with these three options:

Use the arrow keys to navigate left and right, or press the letter that the word begins with. Save and Exit are self-explanatory, but if you wish to have your program neatly set out on paper for storage (Figure 2-12), you can select the Print option.

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_19_1.png)

*Figure 2-12. Printing*

You will need a printer attached with ink sacs and some paper (Figure 2-13).

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_20_0.png)

*Figure 2-13. Adding a printer*

### Controlling Redstone with Lua

Now to write our first program. For now we are just going to turn a lamp on, but later we will have password-protected doors and even a Morse code sender.

The first step is to change directory to the folder where you are going to keep all your programs (*mystuff*), by typing:

```
cd mystuff
```

Then, to create and edit the program file, type:

```
edit redstonetest
```

Next, enter the following text into the editor (Figure 2-14):

```lua
rs.setOutput("left", true)
sleep(3)
rs.setOutput("left", false)
```

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_20_1.png)

*Figure 2-14. Controlling Redstone*

After that, save and then exit your program (press Ctrl and select the Save and then the Exit option with the arrow keys).

To run a program, just type its name to run it. But first, place a Redstone lamp in the left-hand side of the computer like Figure 2-15.

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_21_0.png)

Your lamp should light for three seconds before turning off. Congratulations, you have just written your first program in ComputerCraft!

### ComputerCraft Monitors

Monitors are very handy, especially touchscreen ones which have been recently added, but more of that later. The crafting recipes for a normal and an advanced monitor are shown in Figures 2-16 and 2-17 (advanced monitors are touchscreen-enabled unlike standard ones).

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_21_1.png)

*Figure 2-16. The Monitor recipe*

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_22_0.png)

*Figure 2-17. The Advanced Monitor recipe*

You can place monitors next to each other to make even bigger screens like Figure 2-18.

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_22_1.png)

*Figure 2-18. Big Monitors*

To output to a monitor, type in *monitor* then the side the monitor is on, and then the name of the program, so it could look like this: *monitor left test* (Figure 2-19).

However, if you wish to input via text, you will need to do so through the computer, and not the monitor.

![](img/7ea6f60bb53ecc17dd8979f66d5502d6_22_2.png)

*Figure 2-19. Using a Monitor*

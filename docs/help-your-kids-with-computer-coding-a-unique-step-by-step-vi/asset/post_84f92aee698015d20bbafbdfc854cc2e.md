
# Creating blocks

To avoid repeating the same set of blocks over and over again, it is possible to take a shortcut by creating new blocks. Each new block can contain several different instructions.

# Making your own block

You can make your own blocks in Scratch that run a script when they're used. Try this example to see how they work. Programmers can use these reusable pieces of code as "subprograms" or "functions".

- **Create a new block**
Click on the "More Blocks" button, and select "Make a Block". Type the word "jump" and click "OK".

- **New block appears**
Your new block "jump" appears in the blocks palette, and a "define" block appears in the scripts area.

![](img/72d218a7a73c4d4abc7be582ebd85385_73_0.png)

| Scripts | Costumes | Sounds |
|---|---|---|
| Motion | Events | |
| Looks | Control | |
| Sound | Sensing | |
| Pen | Operators | |
| Data | More Blocks | |

![](img/72d218a7a73c4d4abc7be582ebd85385_73_1.png)

Click here to make a new block

- **Define the block**
The "define" block tells Scratch which blocks to run when using the new block. Add this script to define the block.

- **Use the block in a script**
The new block can now be used in any script. It's as if jumping blocks were in the script individually.

```
define jump
change y by 50
wait 1 secs
change y by -50
```

```
when clicked
forever
jump
wait 1 secs
```

Starts your block definition

Jumps up

The new block runs the jumping script that has already been defined

Drops down

Waits 1 second before repeating the loop

# Blocks with inputs

Windows in a new block can be used to give it numbers and words to work with. These holes can be used to change how far the block moves a sprite.

![](img/72d218a7a73c4d4abc7be582ebd85385_74_0.png)

Click here to see all of the options

- **Make a new block**
Make a new block called 'slide' and then click on 'Options': Select 'Add number input' and type 'steps'. Select 'Add label text' and change it to 'and shout'. Click 'Add string input' and call it 'greeting'. Then click 'OK'.

- **Define the block**
In the 'define' block, the holes are replaced with variables called 'steps' and 'greeting'. Drag variables from the 'define' block into the script wherever you need them. Add this to your script to your sprite.

![](img/72d218a7a73c4d4abc7be582ebd85385_74_1.png)

The steps variable

The greeting variable

> Drag variables from the 'define' block into the script

- **Use the block in a script**
Now add the below script to a sprite. By putting different numbers of steps and greetings into the block, you can make your sprite behave differently.

![](img/72d218a7a73c4d4abc7be582ebd85385_74_2.png)

This block makes the number of steps negative

> Use a sensible name for a new block so the program will be easier to read and change.

```
when space key pressed
slide 20 and shout hello
wait 1 secs
slide 80 and shout how's it going?
```

Starts the script when the spacebar is pressed

The sprite slides 20 steps and shouts "hello"

Now the sprite slides 80 steps and shouts "how's it going?"

# Monkey mayhem

This exciting, fast-paced game brings together all of the Scratch skills you've learned so far. Follow these steps to create your very own “Monkey mayhem” and see if you can hit the bat with the bananas!

# Getting started

Start a new Scratch project. The cat sprite isn't for this project. To remove it, right-click on it in the sprite list and click “delete” in the menu. This will leave you a blank project to work on.

- Add a new backdrop from the backdrop library. This button is found to the left of the sprite list.

Stage
1 backdrop

Click here to add a new backdrop from the backdrop library

New backdrop:

- Double-click to select the “wall1” backdrop. The brick wall works well for this game, but if you prefer, you could use a different backdrop instead.

> SEE ALSO
40–41 Costumes
38–39 Making things move
66–67 Sensing and detecting

# EXPERT TIPS

# Avoiding errors

This is the biggest Scratch program you've tried so far, so you might find that the game doesn't always work as you expect it to. Here are some tips to help things run smoothly:

- Make sure you add scripts to the correct sprite.
Follow the instructions carefully. Remember to make a variable before using it.
- Check that all the numbers in the blocks are correct.

![](img/72d218a7a73c4d4abc7be582ebd85385_75_0.png)

Double-click on a backdrop in the backdrop library to make it appear on the stage

# MONKEY MAYHEM

Go to the sprite library to add a new sprite to the game. Select "Monkey1" from the "Animals" section. The user will control this sprite in the game.

| Sprites | New sprite: |
|---|---|
| Monkey1 | |

Click here to choose a new sprite from the library

Give the monkey script below. Remember—all the blocks can be found in the blocks palette, organized by color. "Sensing" blocks are used to move the monkey around the stage using the arrow keys. Run the script when you've finished to check it.

> This "Motion" block keeps the monkey upright

The arrow keys on the keyboard will make the monkey left and right

- when clicked
set rotation style left-right
go to x: 0 y: (-90)

Moves the monkey to start position at the bottom of the stage

This "Sensing" block detects when the left arrow is pressed

- if arrow pressed?
point in direction (-90)
move 10 steps
next costume

90 makes the monkey point to the left

This makes the monkey look like it is walking by switching costumes

- if arrow pressed?
point in direction (90)
move 10 steps
next costume

90 makes the monkey point to the right

Moves the monkey 10 steps

Don't forget to save your work

# STARTING FROM SCRATCH

# MONKEY MAYHEM

# Adding more sprites

The monkey can now be moved across the stage using the left and right keys. To make the game more interesting, add some sprites. Give some bananas to throw, and a bat to throw them at!

![](img/72d218a7a73c4d4abc7be582ebd85385_77_0.png)

Add the “Bananas” sprite from the sprite library, then give it script. When the game starts, the monkey will hide the bananas. When the spacebar is pressed, they will shoot vertically up the stage. The bananas then reappear at one side of the stage, where they can be picked up again.

```
when clicked
set rotation style left-right
point in direction 0
forever
  repeat until
    go to Monkey 1
    key space?
  repeat 35
    move 10 steps
  if
    pick random 1 to 2 = 1
    go to x: 210 y: -140
  else
    go to x: -210 y: -140
  show
wait until
  touching Monkey 1
```

This makes the bananas stay upright

Sets the bananas' direction to up

This block makes the bananas visible on the stage—they'll be hidden later

The bananas stick to the monkey until the spacebar is pressed

This loop moves the bananas up the stage

This “if-then-else” block makes the bananas reappear on the right or left side of the stage, randomly

This makes the script wait until the monkey picks up the bananas

![](img/72d218a7a73c4d4abc7be582ebd85385_77_1.png)

![](img/72d218a7a73c4d4abc7be582ebd85385_77_2.png)

![](img/72d218a7a73c4d4abc7be582ebd85385_77_3.png)

# MONKEY MAYHEM

The next step is to add a flying bat and make it drop to the ground if it hits the bananas. Add "Bat2" from the sprite library, then create a new variable called "Speed" (for bat only). To create a new variable, first click the "Data" button in the blocks palette, and select the "Make a Variable" button. Use the box by "Speed" variable in the "Data" section so it doesn't appear on the screen.

| New Variable | Name the new variable |
|---|---|
| Variable name: Speed | This variable will only be used with the bat sprite |
| For all sprites | For this only |
| Cloud variable (stored on server) | OK Cancel |

Add the below script to the bat. In the main "forever" loop, the bat moves to a random position on the left of the stage, moves backward and forward across the stage until the bananas hit it. When the bat is hit, it drops to the ground.

![](img/72d218a7a73c4d4abc7be582ebd85385_78_0.png)

```
when clicked
  set rotation style [left-right]
  forever
    go to x: [pick random (1) to (100)] y: [pick random (1) to (20)]
    point in direction [90]
    set [Speed] to
    repeat until [touching Bananas ?]
      move [Speed] steps
      if on edge, bounce
  broadcast [hitbybananas]
  point in direction [180]
  repeat [40]
    move [10] steps
```

> This keeps the bat sprite upright

> The bat starts off on the left of the stage, at a random height

> Sets the bat's direction to right

> Picks a random speed

> This makes the bat moving until it's hit

> Drag the "Speed" variable from the "Data" section into this block

> Create this "broadcast" block to tell other sprites that the bat has been hit. This will be used later in the project

> Sets the direction of the bat to down

> Makes the bat fall down and off the stage

![](img/72d218a7a73c4d4abc7be582ebd85385_78_1.png)


# Party Time!

We've learned a lot about making sprites to do things, but a project isn't complete if it happens on a silent, white stage! Let's see how to give a project some scenery and music from the Scratch libraries to liven things up.

- What You'll Learn:
- How to change the background picture
- How to add effects to the backdrop
- How to add music to your project

![](img/c8b294ee7af329f5e2b96cede7af2ab1_21_0.png)

# Adding Scenery—Backdrops

Just as a sprite can have many costumes, the stage too can have more than one background picture, or backdrop. Click on the **Add new backdrop from library** button at the bottom left of the **Stage info** area.

It's Scratch Cat's birthday, so choose the "party" stage. You'll see the cat on the stage! You can load more than one backdrop. Try loading "underwater2."

![](img/c8b294ee7af329f5e2b96cede7af2ab1_21_1.png)

![](img/c8b294ee7af329f5e2b96cede7af2ab1_21_2.png)

![](img/c8b294ee7af329f5e2b96cede7af2ab1_21_3.png)

# Light Show!

We can add scripts to the stage: click on the small picture of the stage area at the top of the **Stage info** area. Then try running this script with your party backdrop to bring it to life.

![](img/c8b294ee7af329f5e2b96cede7af2ab1_21_4.png)

# Music

A party isn't a party without music!
Sounds can be loaded into a sprite or the stage. But you must make scripts to play them in the Scripts area.

Clicking on the speaker under the Sounds tab will take you to the Sound Library.

# Load Some Music

Click on the stage again. Then click on the Sounds tab above the blocks and select Choose sound from library (the speaker symbol).

New sound:

![](img/c8b294ee7af329f5e2b96cede7af2ab1_22_0.png)

# Select a Tune

Choose one of the music loops, such as “dance funky,” and click OK in the bottom right corner to load. The sound will appear on the list of sounds.

![](img/c8b294ee7af329f5e2b96cede7af2ab1_22_1.png)

# Make, Read, and Run a Script

Click on the Scripts tab and make this script. Read the script and run it. You should have never-ending music!

# Show What You Know

The cat’s in the mood for a party. Are you in the mood for a quiz?

- 1. A background picture on the stage is called a ....................................
- 2. Circle the block that plays a whole sound before continuing: .........................

```
play sound [pop ▼]
play sound [pop ▼] until done
```

- 3. True or False?
a. A project can have only one backdrop loaded. ....................................
b. Only the sprite that loaded a sound can play it. ....................................................
c. The stage can have sounds and scripts. ....................................................
d. Once you’ve chosen a backdrop for a script, you can’t change it. .....................
a. A sprite can use a script to change the stage’s backdrop. .................................

# if-then

If it's raining, we decide to wear a raincoat. We can make this kind of decision in Scratch using the if-then blocks from the yellow Control section. Like loops, they wrap around other blocks and control when they are run.

- What You'll Learn:
- About if-then blocks
- How to control when blocks are run or skipped
- How to sense when keys are pressed

![](img/c8b294ee7af329f5e2b96cede7af2ab1_23_0.png)

# Spin Control

Let's use if-then blocks to decide when our cat spins. We'll use some light blue Sensing blocks, which ask a “true or false?” question. Find them under the Scripts tab.

- Start a New Project
Add this script. What do you think it does? The block inside each if-then block is only run if the answer to the question at the top of the block is “true.”

Cat turns 15 degrees to the left

![](img/c8b294ee7af329f5e2b96cede7af2ab1_23_1.png)

- Run the Script
What happens? Nothing! Press the “a” key and the cat turns backward. Let the key go and it stops. The turn block inside the first if-then block is only run when the answer to the question "key a pressed?" is “true.”

![](img/c8b294ee7af329f5e2b96cede7af2ab1_23_2.png)

Cat turns 15 degrees to the right

- Now Press the “d” Key
The cat turns the other way. The turn block inside the second if-then block is only run when the answer to the question "key d pressed?" is “true.” If neither key is pressed, both blocks are skipped.

![](img/c8b294ee7af329f5e2b96cede7af2ab1_23_3.png)

# A Closer Look at the if-then Block

Look at this if-then block from a script. Read carefully and think about what it does.

If answer's "false," blocks are skipped
Condition (answer is "true" or "false")
If answer's "true," blocks are run

![](img/c8b294ee7af329f5e2b96cede7af2ab1_24_0.png)

- The if-then block is a yellow Control block because blocks inside it are run.
- An if-then block has a question as condition. The question must have a true/false answer.
- The blocks inside the if-then block are only run when the answer to the question is "true."

![](img/c8b294ee7af329f5e2b96cede7af2ab1_24_1.png)

- If the answer to the question is "false," the blocks inside the if-then block are ignored.
- Add this if-then to your script so the cat meows when you press the "s" key. Put the if-then block inside the loop but outside the if-then blocks.

# Show What You Know

If you're a Scratch expert, you'll find this bug easy!
This script should make the sprite change color when you press the space key, but the sprite changes color all the time. Can you spot the "bug"?

![](img/c8b294ee7af329f5e2b96cede7af2ab1_24_2.png)

# Variables

Computers are excellent at storing information, or "data." This data could be someone's name or the weight of a cake. A variable is like a labeled box in which you can store data until your program needs it.

- You'll Learn:
- Variables store data in programs
- How to make and use variables
- Using variables makes code clearer

# A Box with a Label

A variable can store a number or some words (programmers call words a "string"). The thing stored in a variable is called its value. You can change the value of a variable. Give variables helpful names to make the code easy.

![](img/c8b294ee7af329f5e2b96cede7af2ab1_25_0.png)

Follow these instructions to create your first variable in Scratch.

- 1 Start with Data
Select **Data** under the **Scripts** tab. Then click on **Make Variable** button. The **New Variable** window will pop up.

- 2 Name It, Check It, Click It!
First, give your variable a useful name. Check *For all sprites*, and click **OK**. (You can ignore *For this sprite only* and *Cloud variables*.)

![](img/c8b294ee7af329f5e2b96cede7af2ab1_25_1.png)

- 3 Get to Know Your Blocks!
Blocks for this variable will then appear in the blocks area. Make sure you know what each of the blocks does.

Check to show the variable on the stage
The variable block can be used inside other blocks

![](img/c8b294ee7af329f5e2b96cede7af2ab1_25_2.png)

# Countdown Cat

Time to see some variables in action. Start a new project.

In the orange Data section, create two variables called count and message. Always give your variables names that explain what's stored in them.

Add this script. Make sure you drag the little orange blocks with count and message on them into the windows of the say blocks. Don't type the words into the say windows. If you do, the cat will say the variable's name rather than what's stored in the variable.

Read the script. Can you work out what's going to happen? Now run the script.

Experiment with the numbers and text in the script. Can you make the cat count up instead of down?

```
when clicked
set [count] to [10]
set [message] to Blast off!
repeat (10)
say [count] for 1 secs
change [count] by -1
```

![](img/c8b294ee7af329f5e2b96cede7af2ab1_26_1.png)

# See What You Know

Test how much Scratch data you've stored in your brain-box.

- 1. A variable has a name and a ....
- 2. Make a Variable button is found in the orange ... blocks section.
- 3. Fill in the speech bubbles for these sets of blocks:

```
set [name] to Spot!
say [name]
set [name] to Spot!
say [name]
```

![](img/c8b294ee7af329f5e2b96cede7af2ab1_26_2.png)

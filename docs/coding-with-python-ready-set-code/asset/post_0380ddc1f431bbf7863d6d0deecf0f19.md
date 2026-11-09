
## POPPY FLOWER

### IT'S TIME FOR SOME FLOWER POWER!

### READY

You're going to draw a poppy using functions and loops.

Poppies come in many different colors, such as white, pink, yellow, orange, red, or blue.

![](img/a1849c7d7e98817476d64684d9c96952_21_0.png)

### 1 GETTING STARTED

Go to Trinket: https://trinket.io/ and log in.

Type in your username and password.

### SET

### 2 OPEN A NEW TRINKET

Click on **New Trinket** and click on Blocks.

![](img/a1849c7d7e98817476d64684d9c96952_21_1.png)

You will see the following window.

Click on **Turtle**.

You will drop the blocks for your program in this white canvas.

From the Turtle menu, select **shape**. Click on the drop-down menu and select **circle**. We will use a circle to create our flower pattern.

![](img/a1849c7d7e98817476d64684d9c96952_22_0.png)

**Did you know?**

The Golden Poppy, or California Poppy, is the Californian state flower. It grows wild throughout California and became the state flower in 1903.

![](img/a1849c7d7e98817476d64684d9c96952_22_1.png)

### CODE!

You can draw your poppy using lots of different circles.

![](img/a1849c7d7e98817476d64684d9c96952_22_2.png)

**Did you know?**

Every year, on November 11, people remember the end of the First World War. The common field poppy has become a symbol of this remembrance because these flowers began to grow in the fields of battle when the war ended.

### 3 WRITE IN PYTHON

Add this block to your program:

- Press **Run** to test your program.
- You should see a large circle on the right of your screen.

![](img/a1849c7d7e98817476d64684d9c96952_22_3.png)

```python
stamp Circle()
color 100
```

### 4. MAKE A PETAL

The circle has no color inside and is a bit big for the screen. Let's fix this by adding the following blocks to your program:

Change this number by clicking inside the box and typing over the old number with the new one.

Press ▶ Run to test your program.

```
shape circle
begin fill
set color to [red]
circle 25
end fill
```

![](img/a1849c7d7e98817476d64684d9c96952_23_0.png)

You should see a red circle on your screen.

### 5. CREATE A FUNCTION

Click on Functions and add the "do something" block to your program.

![](img/a1849c7d7e98817476d64684d9c96952_23_1.png)

### 6. NAME THE FUNCTION

It is important to name the function so you know what you can do with it. Click inside the box which says "do something," delete, and type "Petal". After that, click on Functions again and you will see a block called "Petal". This is the function you have just created.

From now on, every time you want to draw a petal, you will only need to use the function Petal.

![](img/a1849c7d7e98817476d64684d9c96952_23_2.png)

### USE LOOPS

A poppy has four petals. Programmers can use loops to repeat the same instruction many times. Add the following code to your program using the Functions, Loops, and Turtle menus:

Press ▶ Run to test your program.

You should see a red flower on the right of your screen.

```
repeat 4 times
    do Petal
    turn right by 90
```

Function

```
to Petal
    shape circle
    begin fill
    set color to red
    circle 25
    end fill
```

Program

```
repeat 4 times
    do Petal
    turn right by 90
```

![](img/a1849c7d7e98817476d64684d9c96952_24_0.png)

### CREATE THE CENTER

You will have to add another circle to make the center of the flower. This time the circle will be black. Add the following blocks to your program:

Press ▶ Run to test your program.

This position block will place the black circle right on the center of the flower.

```
repeat 4 times
    do Petal
    turn right by 90
goto 0 -15
set color to black
begin fill
circle 15
end fill
```

### 9. ADD THE STEM

To finish your flower, you need to add the stem. Add the following blocks to your program to finish the poppy:

This block will make the program stop drawing.

This block will make the program continue drawing. Remember to use the drop-down menu to select it.

Press ▶ Run to test your program.

Your program should look like this:

![](img/a1849c7d7e98817476d64684d9c96952_25_0.png)

![](img/a1849c7d7e98817476d64684d9c96952_25_1.png)

### 10. USE TEXT BLOCKS

In Trinket, you can use Text blocks to write a message at the bottom of your screen.

Use these two blocks to write your message.

Press ▶ Run to test your program.

![](img/a1849c7d7e98817476d64684d9c96952_25_2.png)

![](img/a1849c7d7e98817476d64684d9c96952_25_3.png)

### TROUBLESHOOTING

If the petals are too small, you need to change the size of the circle in the function.

![](img/a1849c7d7e98817476d64684d9c96952_26_0.png)

![](img/a1849c7d7e98817476d64684d9c96952_26_1.png)

**Did you know?**

The Bluebonnet Poppy is the state flower of Texas. They are easily found in fields and along roadsides throughout central and southern Texas.

### CHALLENGE

Use your knowledge about functions to create a Golden Poppy (see page 20) and a Bluebonnet Poppy (see above). Use the "set color" block to change the poppy's color and the "change size by" block to change the petals' size.

![](img/a1849c7d7e98817476d64684d9c96952_26_2.png)

## THE CATERPILLAR

### GET READY FOR CREEPY CRAWL FUN!

### READY

You're going to create a program using variables and loops to draw a caterpillar.

**Did you know?**

A caterpillar is the larva of a moth or butterfly. Caterpillars eat a lot of food before producing a hard, outer shell called a chrysalis. Inside the chrysalis, the caterpillar develops into a butterfly.

![](img/a1849c7d7e98817476d64684d9c96952_27_0.png)

### 1. GETTING STARTED

Go to Trinket: https://trinket.io/ and log in.

Type in your username and password.

### The life cycle of a butterfly

- **1. Egg**: The female lays lots of little round eggs and attaches them to leaves or stems.
- **2. Caterpillar (or larva)**: The eggs develop into caterpillars.
- **3. Chrysalis (often called the pupa)**: This is a rest stage in which the caterpillar develops a hard, outer case. Inside the chrysalis, the caterpillar changes and becomes a butterfly.
- **4. Butterfly**: Once the butterfly is ready to emerge, the case around the chrysalis splits open.

![](img/a1849c7d7e98817476d64684d9c96952_27_1.png)

### SET

### 2 OPEN A NEW TRINKET

Click on `New Trinket` and click on Turtle.

![](img/a1849c7d7e98817476d64684d9c96952_28_0.png)

Click on Turtle.

![](img/a1849c7d7e98817476d64684d9c96952_28_1.png)

The following menu will open. Drag the `shape: turtle` block to the white canvas and choose triangle from the drop-down menu.

A variable is a space in the computer memory where you can store information such as numbers, text, or lists of numbers and text. To create a variable you need to name it.

### CODE!

![](img/a1849c7d7e98817476d64684d9c96952_29_0.png)

### CREATE VARIABLES

Click on the Variables menu and then select "Make a Variable".

The following message will appear at the top of the screen:

![](img/a1849c7d7e98817476d64684d9c96952_29_1.png)

Type "x" and click OK. "x" is the name of the variable and it will appear in the Variables menu, like this:

![](img/a1849c7d7e98817476d64684d9c96952_29_2.png)

Add two more variables: one named x and the other named y.

### USE VARIABLES

Drag and drop the block from the Variables menu under the shape block. Click on the drop-down menu and choose x.

Then go to the Numbers menu. Select and drag the first block into your program and type in 150.

Add another two blocks from the Turtle menu to your program:

![](img/a1849c7d7e98817476d64684d9c96952_29_3.png)

This variable will make the triangle move along the screen horizontally.

![](img/a1849c7d7e98817476d64684d9c96952_29_4.png)

![](img/a1849c7d7e98817476d64684d9c96952_29_5.png)

Coordinates in programming are the number of pixels (each small block of color which forms a picture) across the screen (horizontally) and the number of pixels down (vertically).

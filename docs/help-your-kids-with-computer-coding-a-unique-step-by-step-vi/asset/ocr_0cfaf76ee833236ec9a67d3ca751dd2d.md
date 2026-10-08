# # Escape the dragon!

This project introduces some basic Scratch coding. It shows how to make a game to help the cat sprite dodge a fire-breathing dragon.

# ## Make the cat move

This stage explains how to make the cat sprite move around and chase the mouse-pointer. Follow the instructions carefully because the game might not work.

+   1 Open Scratch. Click "File" on the menu and select "New" to start a new project. The cat sprite appears.

+   2 Click the yellow "Control" button in the blocks palette. Then click the "forever" block, keep the mouse button down, and drag the block into the scripts area on the right. Release the button to drop the block.

![](bbox=[0.05, 0.555, 0.255, 0.695])

![](bbox=[0.545, 0.275, 0.945, 0.295])

![](bbox=[0.585, 0.305, 0.935, 0.475])

```
wait 10 secs
repeat 10
forever

forever
```

Drag the block into the scripts area

![](bbox=[0.765, 0.565, 0.915, 0.685])

+   3 Click the blue "Motion" button in the blocks palette. The blue "Motion" commands will appear. Drag the "point toward" block into scripts area and drop it inside the "forever" block. Click the block arrow in the block and choose "mouse-pointer".

+   4 Click the "Events" button in the blocks palette. Drag thewhen green flag clicked" block into the scripts area. Join it to the top of your script.

This block snaps to the top of the script

![](bbox=[0.065, 0.835, 0.485, 0.945])

```
clicked
forever
point towards mouse-pointer
```

The menu shows "mouse-pointer" has been chosen
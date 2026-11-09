# ### 5. Create a box for the interface

Now that you’ve planned what the interface will look like, you can create the rectangular boxes that will make up the GUI. Type this code below what you typed in Step 2 to create a box for the main question.

```
```python
WIDTH = 1280
HEIGHT = 720

main_box = Rect(0, 0, 820, 240)
```
```

This function takes four parameters. The first two numbers are the coordinates of the top-left corner of the box, and the last two numbers are the coordinates of the bottom-right corner of the box.

This sets the box size to 820 pixels wide and 240 pixels high.

# ### 6. Make the other boxes

You now need to make a box for the timer and four separate boxes for each of the answer boxes. Type the code under what you wrote in Step 5.

```
```python
main_box = Rect(0, 0, 820, 240)
timer_box = Rect(0, 0, 240, 240)
answer_box1 = Rect(0, 0, 495, 165)
answer_box2 = Rect(0, 0, 495, 165)
answer_box3 = Rect(0, 0, 495, 165)
answer_box4 = Rect(0, 0, 495, 165)
```
```

The timer box is a square 240 pixels wide and 240 pixels high.

All the answer boxes are the same size.

# ### 7. Move the boxes

At the moment, all the boxes will be drawn on top of each other in the top-left corner. You need to add some code to move them to their correct positions on the screen. Type this code immediately after the code from Step 6.

```
```python
answer_box4 = Rect(0, 0, 495, 165)

main_box.move_ip(50, 40)
timer_box.move_ip(990, 40)
answer_box1.move_ip(50, 358)
answer_box2.move_ip(735, 358)
answer_box3.move_ip(50, 538)
answer_box4.move_ip(735, 538)
```
```

> > Arr! Time to move all these boxes into place!

move_ip() moves each rectangle to the place you want it on the screen.

The top-left corner of each box will be placed at the coordinates in the brackets.

![](bbox=[0.044, 0.704, 0.812, 0.963])